# Setting Up NFS/AutoFS

*The Network File System (NFS) is a mechanism for storing files on a network. It is a distributed file system that allows users to access files and directories locaated on remote computers and treat those files and directories as if they were local. AutoFS is a service that automatically mounts (and unmounts) filesystems when accessed, making NFS storage more efficient.*

---

## Step 1: Set Up the NFS Server

1. **Install NFS Server Tools**
```bash
sudo yum install nfs-utils
sudo systemctl enable --now nfs-server
```

2. **Create a Shared Directory**
```bash
sudo mkdir -p /srv/nfs/shared
sudo chown nfsnobody:nfsnobody /srv/nfs/shared
```

3. **Configure Exports**
Edit /etc/exports:
```bash
/srv/nfs/shared 192.168.1.0(rw,sync,no_subtree_check)
```
Replace 192.168.1.0 with your client's subnet.

Apply the changes:
```bash
sudo exportfs -ra
```

Allow NFS traffic through firewall:
```bash
sudo firewall-cmd --add-service=nfs --permanent
sudo firewall-cmd --reload
```

## Step 2: Set Up the NFS Client

1. **Install NFS Client Tools**
```bash
sudo yum install nfs-utils
```

2. **Test the Mount** (optional)
```bash
sudo mount -t nfs server_ip:/srv/nfs/shared /mnt
```
You should see the shared fiels under /mnt.

## Step 3: Configure AutoFS on the Client

1. **Install autoFS**
```bash
sudo yum install autofs
```

2. **Configure AutoFS Maps**
Edit /etc/auto.master and add this line:
```bash
/nfs /etc/auto.nfs
```

Create /etc/auto.nfs
```bash
shared -rw,soft,intr server_ip:/srv/nfs/shared
```
This tells AutoFS to mount `server_ip:/srv/nfs/shared` when accessed.

3. **Restart AutoFS**
```bash
sudo systemctl restart autofs
```

4. **Test the Mount**
```bash
ls /nfs/shared
```
It should auto-mount the directory. If unused for a few minutes, AutoFS will unmount it automatically.

## Things to Keep in Mind
- AutoFS works in tandem with NFS, rather than replacing it.
- Be careful with syntax and spacing in nfs configuration files.

## Resources
**History:**
- [NFS: the early years](https://lwn.net/Articles/897917/)
- [NFS: the new millennium](https://lwn.net/Articles/898262/)

**How-To:**
- [How NFS Works](https://tldp.org/LDP/nag/node140.html)
- [Rocky Linux Guide to NFS](https://docs.rockylinux.org/guides/file_sharing/nfsserver/)
- [Guide to AutoFS](https://www.linuxtechi.com/automount-nfs-share-in-linux-using-autofs/)
- [Automounting Guide](https://www.ucartz.com/clients/knowledgebase/1234/Beginners-Guide-to-Automounting-File-Systems-in-CentOS-or-RHEL.html)

**Literature:**
- [Linux NFS Documentation](https://wiki.archlinux.org/title/NFS)
- [NFS Man Page](https://linux.die.net/man/5/nfs)
- [Exports Man Page](https://linux.die.net/man/5/exports)
- [AutoFS Man Page](https://linux.die.net/man/5/autofs)
