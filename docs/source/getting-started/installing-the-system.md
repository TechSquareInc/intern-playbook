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

### Linux Boot Process

The [Linux boot process](https://en.wikipedia.org/wiki/Booting_process_of_Linux) is a series of steps a Linux system follows to initialize hardware and start the operating system after a computer is powered on or restarted. The boot process happens in six key stages:

1. **BIOS/UEFI:** Initializes the hardware and looks for a boot device.
2. **Bootloader:** Loads and starts the Linux kernel.
3. **Kernel:** Initializes device drivers and mounts the root filesystem.
4. **Initramfs:** Temporary filesystem loads into memory which prepares the real root filesystem to be mounted.
5. **Init System:** System initialization which starts the essential system services such as for networking, loggingm or user management.
6. **User Login:** Once `init` process is complete, the system presents a login screen, allowing users to log in and access the system.

![linux boot process](https://media.licdn.com/dms/image/v2/D5622AQEbxeHiI27Q-g/feedshare-shrink_800/B56ZfPDY3xHoAk-/0/1751525463324?e=1755129600&v=beta&t=XLqwKaY4Weadjf5gp1W8t3QZTDS3H6iZX1d--ccFw3c)

### Resources
- [Linux Distributions](https://en.wikipedia.org/wiki/List_of_Linux_distributions): A list of all of the different linux distributions.
- [Linux Distribution](https://en.wikipedia.org/wiki/Linux_distribution): In-depth exploration of what a Linux distribution is.
- [Linux Boot Process](https://www.youtube.com/watch?v=XpFsMB6FoOs): High level overview of the Linux boot process.
- [Booting Process of Linux](https://en.wikipedia.org/wiki/Booting_process_of_Linux): In-depth exploration of the Linux boot process.
