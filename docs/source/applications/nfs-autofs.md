# Setting Up NFS/AutoFS

*The Network File System (NFS) is a mechanism for storing files on a network. It is a distributed file system that allows users to access files and directories located on remote computers and treat those files and directories as if they were local. AutoFS is a service that automatically mounts (and unmounts) filesystems when accessed, making NFS storage more efficient.*

---

## Step 1: Set Up NFS Export on Server
Setup NFS server named (server) on a VM and share `/home` to only the client.

1. **Install NFS Server Tools and NFS Server**
```bash
sudo yum install nfs-utils
sudo yum install nfs-kernel-server
```

2. **Configure Exports**

Add the export rule to `/etc/exports`:

```bash
/home client_IP(rw,sync,no_subtree_check)
```
- Replace `client_IP` with the actual IP or hostname of the client.

3. **Restart the Service**
```bash
sudo systemctl restart nfs-kernel-server
```


## Step 2: Set Up User on Server

1. **Create `tsqaure` User on Server**
```bash
sudo useradd -m -d /home/tsquare tsquare
sudo passwd tsquare
```
- This user's home folder now lives on the NFS-exported directory `/home`.

## Step 3: Mount Export on Client

1. **Install NFS Client**
```bash
sudo yum install nfs-common
```

2. **Mount the NFS Share**
```bash
sudo mount server:/home /mnt/home
```

## Step 4: Enable Persistence via `/etc/fstab`

1. **Make `/mnt/home` Permanent Across Reboot (on client)**

- Edit the `/etc/fstab` and add:

```bash
server:/home	/mnt/home	nfs	defaults	0 0
```
- This ensures it mounts on boot.

## Step 5: Add Client User Pointing to Mounted Home

1. **Add a User to (client) and Make `/mnt/home` their Home Directory**

- Let's say the user is `tsquare`, and their home is mounted over NFS:

```bash
sudo user add -d /mnt/home/tsquare -s /bin/bash tsquare
sudo passwd tsquare
```
- Now when `tsquare` logs in, it uses `/mnt/home/tsquare` as their home, backed by the NFS share.

## Step 6: Migrate NFS Mount

1. **On (client) Migrate `/mnt/home` to `/home` and Retain Permanent Users**
- This means you want the server's `/home` (shared via NFS) to be mounted as the local `/home` directory on the client. Start by unmounting `/mnt/home`:
```bash
sudo umount /mnt/home
```

- Update `/etc/fstab`:
```bash
server:home	/home	nfs	defaults	0 0
```

- Mount it:
```bash
sudo mount -a
```

- Now the `/home` directory on the client is actually coming from the server via NFS.

> **Note:** You must create the `tsquare` user on the client with the same UID/GID as on the server.

```bash
sudo useradd -u [UID] -g [GID] -d /home/tsquare -s /bin/bash tsquare
```
- Use `id tsquare` on the server to fidn UID/GID.
- This ensures correct ownership of files when `tsquare` logs into the client.

## Step 7: Use AutoFS for Dynamic Mounting
Setup autofs on (client) so that `/server/home` works. This uses autofs to mount the NFS share on demand.

1. **Install AutoFS**
```bash
sudo yum install autofs
```

2. **Edit `/etc/auto.master` and Add**
```bash
/server	/etc/auto.home
```

3. **Create `/etc/auto.home`:**
```bash
home	-fstype=nfs	server:/home
```

4. **Restart AutoFS**
```bash
sudo systemctl restart autofs
```
- Now when you `cd /server/home`, autofs automatically mounts it.

## Step 8: Enable Root Access

Share `server:/home` with your desktop so root can write a file to `/home/root` as root. On the server:

1. **Allow Root Access in `/etc/exports`**
```bash
/home	desktop_IP(rw,sync,no_subtree_check,no_root_squash)
```
> **Note:** `no_root_squash` lets the remote root user act as root on the share -- use with caution!

2. **Mount the Share and Write as Root**
- On the desktop:
```bash
sudo mount server:/home /mnt/home
sudo touch /mnt/home/root/hello.txt
```


## Things to Keep in Mind
- AutoFS works in tandem with NFS, rather than replacing it.
- Be careful with syntax and spacing in nfs configuration files.

---
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
