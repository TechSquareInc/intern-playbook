# Using Checkmk

*Checkmk is an open source software designed for monitoring IT systems such as containers, servers, and databases.*

---

## What is Checkmk?
[Checkmk](https://docs.checkmk.com/latest/en/welcome.html) is an open-source (and enterprise) IT monitoring system that helps monitor servers, applications, network devices, containers, cloud infrastructure, and more. It is also known for auto-discovery of services, efficient monitoring engine, custome plugins and dashboards, and email/SMS/Slack alerts.

### Installation
1. Checkmk requires a number of software packages from your Linux distribution. To make sure all the necessary packages are installed, you'll need a correct configuration of the software sources.

For Rocky 9.x, you'll use `https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm`.
```bash
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
```

2. You will need to enable the `subscription-manager` repository on RHEL-based Linux systems using:
```bash
subscription-manager repos --enable "codeready-builder-for-rhel-8-x86_64-rpms"
```

3. Setup SELinux and Firewall:
As a first step, you will need to allow your web server to access the network interfaces.
```bash
setsebool -P httpd_can_network_connect 1
```

Secondly, release the web server and activate this chagnge.
```bash
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --reload
```

4. Download the appropriate packages. Checkmk Raw is the free and open source option:
```bash
wget https://download.checkmk.com/checkmk/2.4.0p6/check-mk-raw-2.4.0p6-el9-38.x86_64.rpm
```
**Note:** This step will likely take a while, so be prepared to wait for its installation to finish. 

5. Signed-package Installation
All Checkmk packages are signed using GnuPG. So that these signed packages can be installed in their ususal way, you will need to import the public key so that the signature is trusted.
```bash
wget https://download.checkmk.com/checkmk/Check_MK-pubkey.gpg
```

Next, import the key to the list of trusted signatures:
```bash
rpm --import Check_MK-pubkey.gpg
```

Once you the key has been imported, you can verify the package and install it:
```bash
rpm -K check-mk-raw-2.4.0p4-el8-38.x86_64.rpm
yum install check-mk-raw-2.4.0p4-el8-38.x86_64.rpm
```

6. Test Installation
If  successful, you will see install version by running:
```bash
omd version
```

## Monitoring


## Resources
- [Install Guide](https://docs.checkmk.com/latest/en/install_packages_redhat.html): Install options for RHEL/CentOS
- [Checkmk on the Command Line](https://docs.checkmk.com/latest/en/cmk_commandline.html): Using chceckmk via the cli
- [Basic Information on the Installation of Checkmk](https://docs.checkmk.com/latest/en/install_packages.html): Installation and use guide
- [Checkmk Welcome Guide](https://docs.checkmk.com/latest/en/welcome.html): Welcome guide to using Checkmk
