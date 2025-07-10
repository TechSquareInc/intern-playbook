# ⚠️  Using Checkmk

*Checkmk is an open source software designed for monitoring IT systems such as containers, servers, and databases.*

---

## What is Checkmk?
[Checkmk](https://docs.checkmk.com/latest/en/welcome.html) is an open-source (and enterprise) IT monitoring system that helps monitor servers, applications, network devices, containers, cloud infrastructure, and more. It is also known for auto-discovery of services, efficient monitoring engine, custom plugins and dashboards, and email/SMS/Slack alerts.

### Installation
1. Checkmk requires a number of software packages from your Linux distribution. To make sure all the necessary packages are installed, you'll need a correct configuration of the software sources.

For Rocky 9.x, you'll use `https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm`.
```bash
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
```

2. You will need to enable the CodeReady Builder repository on Rocky 9 Linux systems using:
```bash
sudo dnf config-manager --set-enabled crb
```

3. Setup SELinux and Firewall:

As a first step, you will need to allow your web server to access the network interfaces.
```bash
setsebool -P httpd_can_network_connect 1
```

Secondly, release the web server and activate this change.
```bash
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --reload
```

4. Download the appropriate packages. Checkmk Raw is the free and open source option:
```bash
wget https://download.checkmk.com/checkmk/2.4.0p6/check-mk-raw-2.4.0p6-el9-38.x86_64.rpm
```
> **Note:** This step will likely take a while, so be prepared to wait for its installation to finish.

5. Signed-package Installation:

All Checkmk packages are signed using GnuPG. So that these signed packages can be installed in their ususal way, you will need to import the public key so that the signature is trusted.
```bash
wget https://download.checkmk.com/checkmk/Check_MK-pubkey.gpg
```

Next, import the key to the list of trusted signatures:
```bash
rpm --import Check_MK-pubkey.gpg
```

Once the key has been imported, you can verify the package and install it:
```bash
rpm -K check-mk-raw-2.4.0p6-el9-38.x86_64.rpm
yum localinstall check-mk-raw-2.4.0p6-el9-38.x86_64.rpm
```

6. Test Installation:

If  successful, you will see install version by running:
```bash
omd version
```

### Monitoring

Monitoring with Checkmk can be described as a comprehensive, modular, and efficient way to keep track of the health and performance of IT systems. It involves setting up a centralized monitoring server to collect, visualize, and alert on system metrics and service statuses. It provides real-time insights, automated service discovery, and customizable alerts, which enables system administrators to detect issues before they become a more serious problem.

Checkmk offers monitoring services for everything from servers, networks, applications, databases, cloud infrastructures and more. Learn more about Checkmk's various monitoring solutions by visting their [Monitoring Basics](https://checkmk.com/monitoring) page.

#### Monitoring Tutorial

**Objective**: Set up a monitoring environment using Checkmk Raw Edition to monitor a virtual machine.

- Create or use a already configured virtual machine, and using Checkmk's documentation, add that machine as a host to Checkmk.
- Use [Checkmk site creation docs](https://docs.checkmk.com/latest/en/omd_basics.html) to create a site, and add your host to the site.
- Use [Checkmk on the Command Line](https://docs.checkmk.com/latest/en/cmk_commandline.html) to explore monitoring configurations.

For more explicit help on this, check out Checkmk's official [Installing Checkmk and Monitoring your First Host Tutorial](https://www.youtube.com/watch?v=opO-SOgOJ1I).


## Resources
- [Install Guide](https://docs.checkmk.com/latest/en/install_packages_redhat.html): Install options for RHEL/CentOS
- [Checkmk on the Command Line](https://docs.checkmk.com/latest/en/cmk_commandline.html): Using chceckmk via the cli
- [Basic Information on the Installation of Checkmk](https://docs.checkmk.com/latest/en/install_packages.html): Installation and use guide
- [Checkmk Welcome Guide](https://docs.checkmk.com/latest/en/welcome.html): Welcome guide to using Checkmk
- [Site Admistration with `omd`](https://docs.checkmk.com/latest/en/omd_basics.html): Explore Checkmk's site creation guide.
- [Monitoring Basics](https://checkmk.com/monitoring): Explore Checkmk's monitoring basics guide.
- [Monitoring Linux](https://docs.checkmk.com/latest/en/agent_linux.html): Explore monitoring a Linux agent.
