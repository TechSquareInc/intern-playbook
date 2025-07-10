# 🖥️ Setting up a KVM Virtual Machine

*This guide walks you through installing KVM and Libvirt tools on your Linux desktop, and creating a virtual machine.* 

---

## Step 1: Install KVM, Libvirt, and Virt-Manager
1. Check that your hardware supports virtualization:
```bash
egrep -c '(vmx|svm)' /proc/cpuinfo
```
- The output of that command should reflect the total number of logical CPU cores available. 
- This command is taking a count of the number of CPU cores that support hardware virtualization:
	- `vmx`=Intel VT-x support (for Intel CPUs)
	- `svm`=AMD-V support (for AMD CPUs)

2. Install the necessary packages to enable virtulization and manage VMs:
```bash
sudo yum install virt-manager libvirt libvirt-daemon-kvm qemu-kvm
```
- `virt-manager` is a desktop user interface for managing virtual machines through `libvirt`
- `libvirt` is an open-source API, daemon, and managment tool for managing platform virtualization across different hypervisors like KVMs
- `libvirt-daemon-kvm` refers to the `libvirtd` daemon, which is part of the libvirt virtualizatoin managment system, and is specifcally configured to manage KVMs (Kernel-based Virtual Machine).
- `qemu-kvm` is a package that integrates QEMU (Quick Emulator) and KVM to enable efficient virtualization on Linux systems.

3. Enable `libvirtd` by running:
```bash
sudo systemctl enable libvirtd
```

## Step 2: Verify Installation
1. Check if KVM is available:
```bash
lsmod | grep kvm
```

2. Check if `libvirtd` is running:
```bash
sudo systemctl status libvirtd
```

## Step 3: Create a Virtual Machine
1. Open the `virt-manager` GUI by running:
```bash
virt-manager
```
- By defualt, virt-manager is connected directly to localhost. By right clicking on the localhost (QEMU/KVM), selecting "details", and then the "storage" tab, you can add a new storage volume and allocate space for files stored on your virtual machine.
- Once you have created a new storage volume, you can begin creating a new virtual machine from the main window.
- Follow the steps prompted by the wizard window and specify which local install media you will use. For this project you can use the same ISO image as what is installed on your laptop, or choose a different image.

## Step 4: Enable Networking Between Host and VM
To allow SSH access, configure virtual networking:
- Refer to: [Libvirt Virtual Networking](https://wiki.libvirt.org/VirtualNetworking.html)
- By defualt, virt-manager may already have NAT forwarding enabled.

## Resources
- [How to Install KVM and Libvirt](https://www.howtoforge.com/how-to-install-kvm-and-libvirt-on-centos-6.2-with-bridged-networking): Step by step in depth installation guide for KVM and Libvirt tools
- [How to Create Virtual Machines in Linux Using KVM](https://www.tecmint.com/install-and-configure-kvm-in-linux/): Step by step in depth installation guide for installing and configuring virt-manager application and machines
- [Installing KVM Ubuntu](https://linuxhint.com/install_kvm_ubuntu/): Guide for installing KVM tools and using KVM with virt-manager with Ubuntu
- [Libvirt Virtual Networking](https://wiki.libvirt.org/VirtualNetworking.html): Create a bridged interface so your VM can access the network and internet
