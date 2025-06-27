# Superuser Privileges

The "root" user is the superuser account in Linux systems. Users can temporarily gain root privileges using the `sudo` command, which requires authenticaion from the users account. The user will only have `sudo` privileges if the account is listed in the sudoers file.

---

## Adding a User to the Sudoers File

To add a user to the sudoers file, you will need to edit the `/etc/sudoers` file. As best practice, you should use the `visudo` command to open and edit this file. Typically, you'll add a line specifying the user and their privileges, such as `username	ALL=(ALL:ALL)	ALL`. For more information about the sudoers file, visit [this resource](https://www.linuxfoundation.org/blog/blog/classic-sysadmin-configuring-the-linux-sudoers-file).

## Using the `su` Command

It is highly reccommended that GUI interfaces not be run as root, as this can easily lead to disaster. It is best to be logged in as a normal unprivileged user and to only use `root` as required. Many commands can only be run as the `root` user. To run these commands, use the `su` command (substitute user).

The `su` command takes the following format:

```
su - <user>
```

or 

```
su <user>
```

most commonly you will use `su` to become the `root` user:

```
su - root
```
or 

```
su root
```

If no username is specified, the root user is automatically assumed. For more information on `su` checkout [this resource](https://wiki.centos.org/TipsAndTricks(2f)BecomingRoot.html) or visit the `su` [man pages](https://man7.org/linux/man-pages/man1/su.1.html). 
