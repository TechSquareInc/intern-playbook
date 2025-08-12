# Create Your Own Virtual HPC Cluster

This document outlines the process for setting up a virtualized network for a High Performance Computing cluster. The objective is to establish a virtual network that supports SSH-based management, NFS shared storage, inter-node communication and munge-based authentication for Slurm, with optional support for PXE booting, Kickstart automated install, and Salt configuration management. This is intended for interns and students to learn about systems administration and HPC infrastrucutre.

## Network Architecture
The HPC cluster is composed of the following VM roles:

|VM Name|Role|Services|
|:------|:---|:-------|
|`admin`|SSH, NFS server|NFS, Munge, Slurm client, SSH|
|`controller`|Slurm controller, Munge master|slurmctld, munge|
|`node01`+|Compute nodes|slurmd, munge|

## Step 1: Create a Virtual Network
Learn more about using `libvirt` to create a virtual network by visiting the [libvirt wiki](https://wiki.libvirt.org/VirtualNetworking.html#the-virtual-machine-manager-virt-manager)

### Define Network XML

Create a file and name it something like `cluster-net.xml`
Your XML file may look something like:
```bash
<network>
  <name>hpc-cluster-net</name>
  <forward mode='nat'/>
  <bridge name='virbr10' stp='on' delay='0'/>
  <ip address='192.168.100.1' netmask='255.255.255.0'>
    <dhcp>
      <range start='192.168.100.100' end='192.168.122.200'/>
    </dhcp>
  </ip>
</network>
```

### Create and Start Network

Use [basic command line](https://wiki.libvirt.org/TaskNATSetupVirtManager.html) tools to define and start your cluster.
```bash
sudo virsh net-define cluster-net.xml
sudo virsh net-autostart hpc-cluster-net
sudo virsh net-start hpc-cluster-net
```

Use `virsh net-list --all` to verify the network is created and started.

## Step 2: Create the VMs

Use `virt-manager` or `virt-install` to configure and create VMs attached to the network.
	- `virt-manager` is the graphical user front end for Libvirt which provides virtual machine management.

Download `virt-install` by running:
```bash
sudo yum install virt-install
```

### Download ISO

For this tutorial, download the [Ubuntu Server ISO](https://ubuntu.com/download/server), and be sure to move that file to a location that is readable by the `qemu` user.

```bash
sudo mkdir-p /var/lib/libvirt/boot
sudo cp ~/Downloads/ubuntu-22.04.4-live-server-amd64.iso /var/lib/libvirt/boot/
``` 

### Create your first VM

Use ['virt-install'](https://infotechys.com/create-a-virtual-machine-in-kvm-using-virt-install/) if you prefer to configure network settings from the command line. For example:
```bash
sudo virt-install \
  --connect qemu:///system \
  --name admin \
  --memory 2048 \
  --vcpus 2 \
  --disk size=10 \
  --network network=hpc-cluster-net \
  --os-variant=ubuntu24.04 \
  --noautoconsole
```

### Clone the Admin node

To create your other 2 VMs, you can clone the admin node we just created. First, shut down the `admin` VM temporarily.
```bash
sudo virsh shutdown admin
```
Verify the VM is shut off by running:
```bash
sudo virsh list --all
```

### Clone it to `controller` and `node01`

```bash
sudo virt-clone --original admin --name controller --file /var/lib/libvirt/images/controller.qcow2
sudo virt-clone --original admin --name node01 --file /var/lib/libvirt/images/node01.qcow2
```

And start the new VMs
```bash
sudo virsh start controller
sudo virsh start node01
```

### Reconfigure VM Hostname
For each new VM, access the console and change the hostname:
```bash
sudo hostnamectl set-hostname controller
sudo hostnamectl set-hostname node01
```
And reboot for hostname to take effect:
```bash
sudo reboot
```

### Reset IP on `controller` and `node01`

Because we cloned the `admin` node to the `controller` and `node01`, the IP may appear the same for all nodes. To generate new IPs for the `controller` and `node01`, login to each node and run:
```bash
sudo truncate -s 0 /etc/machine-id
sudo systemd-machine-id-setup
```

You may also need to delete old DHCP leases (if they exist)
```bash
sudo rm -f /var/lib/dhcp/*
sudo rm -f /var/lib/NetworkManager/*lease*
```

Reboot the VM to let them request new DHCP leases
```bash
sudo reboot
```

## Step 3: Set Static IPs and Hostnames

Edit `/etc/hosts` on all nodes to include each VMs IP and hostname:
```bash
192.168.100.1 admin
192.168.100.10 controller
192.168.100.101 node01
```

## Step 4: Setup SSH Key Access

### Generate SSH Key on Your Laptop

```bash
ssh-keygen -t rsa -b 4096
```

### Copy SSH Key to Nodes

```bash
ssh-copy-id user_admin@192.168.100.1 # admin
ssh-copy-id user_admin@192.168.100.10 # controller
ssh-copy-id user_admin@192.168.100.101 # node01
```

### Optional: Setup `~/.ssh/config` on Your Laptop

This will allow you to `ssh` into your nodes from your laptop without open the VM console directly.
```bash
Host admin
  HostName 192.168.100.1
  User user_admin

Host controller
  HostName 192.168.100.10
  User user_admin

Host node01
  HostName 192.168.100.101
  User user_admin
```

## Step 5: Configure NFS Server (on Admin)

### Install and Export Directories
```bash
sudo apt install nfs-kernel-server
sudo mkdir -p /srv/nfs/home
```
Add to `/etc/exports`:
```bash
/srv/nfs/home 192.168.100.0/24(rw,sync,no_subtree_check,no_root_squash)
```
Apply exports:
```bash
sudo exportfs -a
sudo systemctl restart nfs-server
```

### Mount the NFS Share on Compute Nodes

Edit the `/etc/fstab` and add:
```bash
admin/srv/nfs/home	/mnt	nfs	deafults	0	0
```

Create the mount point if it does not exist:
```bash
sudo mkdir -p /mnt
sudo mount -a
```

Verify with:
```bash
mount | grep nfs
```


## Step 6: Setup Munge Authentication
Munge must be installed on all nodes to allow authenicated communication between Slurm components.

### Install Munge on Nodes
```bash
sudo apt update
sudo apt install munge -y
```

### Generate a Munge Key (on admin)
```bash
sudo dd if=/dev/urandom bs=1 count=1024 of=/etc/munge/munge.key
sudo cp /etc/munge/munge.key /tmp/munge.key
sudo chmod 644 /tmp/munge.key
```

### Copy the Munge Key Nodes
```bash
scp /tmp/munge.key controller:/tmp/
scp /tmp/munge.key node01:/tmp/
```

### Move Munge Key to Permanent Location
```bash
sudo mv /tmp/munge.key /etc/munge/munge.key
sudo chown munge:munge /etc/munge/munge.key
sudo chmod 400 /etc/munge/munge.key
```

### Enable and Start Munge on All Nodes
```bash
sudo systemctl enable --now munge
```

## Step 7: Install and Configure Slurm

### Install Slurm
```bash
sudo apt install slurm-wlm
```

### Create Slurm Directories on Controller
```bash
sudo mkdir -p /var/spool/slurmctld
sudo chown slurm:slurm /var/spool
sudo chown slurm:slurm /var/spool/slurmctld
sudo chmod 755 /var/spool /var/spool/slurmctld
```

### Add `slurm.conf` File
```bash
ClusterName=hpc-cluster
ControlMachine=controller
SlurmUser=slurm
SlurmdUser=slurm
StateSaveLocation=/var/spool/slurmctld
SlurmdSpoolDir=/var/spool/slurmd

NodeName=node01 CPUs=2 State=UNKNOWN
PartitionName=debug Nodes=node01 Default=YES MaxTime=INFINITE State=UP
```

### Start the Service on Controller
```bash
sudo systemsctl enable --now slurmctld
```

### On the Compute Node
```bash
sudo mkdir -p /var/spool/slurmd
sudo chown slurm:slurm /var/spool/slurmd
sudo chmod 755 /var/spool/slurmd
```

### Coopy `slurm.conf` from the Controller
```bash
scp controller:/etc/slurm/slurm.conf ~/slurm.conf
sudo mv ~/slurm.conf /etc/slurm/slurm.conf
```

### Start slurmd
```bash
sudo systemctl enable --now slurmd
```

### Test Slurm
```bash
sinfo
srun hostname
```
## Step 8 (Optional): Add SaltStack for Configuration Management

### Download and install Salt Bootstrap

On the Master (Admin Node):
```bash
curl -o bootstrap-salt.sh -L https://github.com/saltstack/salt-bootstrap/releases/latest/download/bootstrap-salt.sh
sudo sh bootstrap-salt.sh -P -M stable 3006.1
```

On the Minions (Controller and Node01):
```bash
curl -o bootstrap-salt.sh -L https://github.com/saltstack/salt-bootstrap/releases/latest/download/bootstrap-salt.sh
sudo sh bootstrap-salt.sh -P stable 3006.1
```

### Enable Salt on Master / Minions

```bash
sudo systemctl enable --now salt-master #master
sudo systemctl enable --now salt-minion #minion
```

### Configure the Salt minion

On each Minion, create and add the file `/etc/salt/minion.d/master.conf`:
```bash
master: admin
```

Then restart the minion:
```bash
sudo systemctl restart salt-minion
```

### Accept the Keys

On the Salt Master:
```bash
sudo salt-key -L # list pending keys (you'll see each minion by its hostname)
sudo salt-key -A # accept all keys
```

### Test Connection
```bash
sudo salt '*' test.ping
```


## Resources
- [Slurm Documentation](https://slurm.schedmd.com/quickstart_admin.html#quick_start)
- [Ubuntu Server Docs](https://documentation.ubuntu.com/server/)
- [Libvirt Networking](https://wiki.libvirt.org/VirtualNetworking.html)
- [PXELINUX/SYSLINUX](https://wiki.syslinux.org/wiki/index.php?title=PXELINUX)
- [Kickstart Installation](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/7/html/installation_guide/sect-kickstart-howto)
- [Munge Installation](https://github.com/dun/munge/wiki/Installation-Guide)
- [dnsmasq Docs](https://thekelleys.org.uk/dnsmasq/doc.html)
- [Bootstap Salt](https://github.com/saltstack/salt-bootstrap/blob/develop/README.rst#install-using-curl)
- [Configure Salt](https://docs.saltproject.io/salt/install-guide/en/latest/topics/configure-master-minion.html)
