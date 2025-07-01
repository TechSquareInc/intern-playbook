# Installing the System

*On your first day, you'll recieve a laptop and a USB stick flashed with a linux distro (likely the latest version of Rocky Linux). However, as you may know, there are a variety of different Linux distributions to choose from. If you are installing a different distro, these instructions may or may not be applicable. This [wikipidea page](https://en.wikipedia.org/wiki/List_of_Linux_distributions)  has a list of different Linux distrubitions to learn more about.*

---

## Installation Procedure

1. Recieve your laptop and USB stick.
2. While the laptop is powered off, insert the USB stick.
3. Power the laptop on and spam the F12 key to enter the boot menu.
4. From here, choose to boot your system from the USB stick.
5. Reclaim whatever space is needed to install the system.
6. Make sure the laptop is connected to wifi to allow for the installation of dependent repositories.
7. Setup Rocky Linux:
	- Create user account
	- Assign root password
8. Click "Begin  Installation" when all setup requirements are filled.

### Optional Additional Resources to Install

- [EPEL](https://fedoraproject.org/wiki/EPEL/FAQ#What_is_EPEL.3F) or Extra Packages for Enterprise Linux. These packages are not part of the main distributions but are often used to enhance or extend the functionality of these systems. Generally speaking, you should run `sudo yum install epel-release` to install.
- [KeePassXC](https://keepassxc.org/download/#linux) a free and open source password manager that allows users to securely store and manage passwords in an encrypted database. Follow this [quick tutorial](https://www.youtube.com/watch?v=NFFSL4YbsOc&t=132s) for installation help.
- [Xfce](https://en.wikipedia.org/wiki/Xfce) a lightweight, modular, customizable, and fast desktop environment for Unix-like operating systems, particularly Linux. It's know for its speed, low resource usage, and stability, making it a good choice for older or less powerful computers.
