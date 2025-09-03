# Setting Up an Apache Web Server

*Apache, or the Apache HTTP Server, is a free and open-source web server software. It is a widley used tool for delivering web content over the internet by acting as a bridge between web servers and users. Essentially, when someone visits a website, Apache is often the software that handles requests and sends the websites's files back to their browser.*

---

## Build a Personal Web Server with Apache

The purpose of this project is to install and configure an Apache HTTP Server on a Linux VM, and serve custom HTML sites.

### Step 1: Create a Linux Virtual Machine

1. Download a Linux ISO, server or desktop, depending on preference. For example, find Ubuntu ISO Downloads [here](https://ubuntu.com/download).
2. Create a VM, attach the ISO, and install the OS. Perform updates to prepare for Apache install.

### Step 2: Install Apache on the Virtual Machine

1. On the VM, run:
```bash
sudo apt install apache2
```

2. Check the service:
```bash
sudo systemctl status apache2
```

3. Find your VM's IP (on local network):
```bash
ip a
```

4. Then open your browser on the host machine and go to:
```bash
http://<vm-ip-address>
```

- You should see the Apache2 default welcome page.

---
## Resoruces
- [How to Deploy Apache Web Server Quickly](https://www.redhat.com/en/blog/install-apache-web-server): Learn to deploy a web server with Apache HTTP Server.
- [Apache HTTP Server Docs](https://httpd.apache.org/docs/2.4/): Apache's offical HTTP Server Documentation.
- [Getting Started with Apache HTTP Server](https://httpd.apache.org/docs/2.4/getting-started.html): Walkthrough the basics of how to get started with Apache HTTP Server.
