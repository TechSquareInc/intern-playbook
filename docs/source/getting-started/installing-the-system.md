# Installing the System

*Linux is a community of free and open-source operating systems used across servers, desktops, and embedded systems. There are many distributions (or distros) to chose from, each with their own unique features, package managers, and system tools.*

---

## Linux and HPC
Linux is the dominant operating system for High Performance Computing clusters, as it provides flexible, customizable, and cost-effective platforms for buidling and managing HPC environments.

## Linux Distributions
While all Linux distributions share the Linux kernel, they can differ slightly in how they handle packages and system configurations. Common Linux families include:

- **Debian** which is known for its stability and ease of use. Some examples include Ubuntu, Linux Mint, or Kali Linux. Debian systems use `.deb` packages and the `apt` package manager.
- **RPM** or the **Red Hat Package Manager** is often favored in enterprise environments, and is used by Rocky Linux, Fedora, Centos, and RHEL. RMP systems use `.rpm` pacakges and package managers like `dnf` or `yum`.
- **Arch** offers cutting edge software on a rolling release model. Arch is known for its minimalistic design, which allows users to customize their system to their exact needs. Arch uses the `pacman` package manager. Some examples include Arch Linux or Manjaro.

## Installation Procedure
These steps apply broadly to installing Linux on a computer uses a USB stick.
1. Create a bootable USB drive: Download an ISO file of your chosen Linux distro and use a tool like Balena Etcher or Rufus to flash it to a USB stick. 
2. While the laptop is powered off, insert the USB stick.
3. Access the boot menu: Power on or reboot your computer, and press the boot menu key (`F12`,`Esc`,`F10`, or similar depending on your system.)
4. Boot from USB: Select the USB stick from the boot menu to load the Linux installer.
5. Start the installation process. Follow the prompts from the installer. Typically this includes:
	- Selecting language and region
	- Setting up a user account
	- Assigning a root password
	- Partitioning or reclaiming disk space
	- Connecting to  a network (important for downloading additional dependent packages)
6. Click "Begin  Installation" when all setup requirements are filled.

### Optional Additional Resources to Install

- [EPEL](https://fedoraproject.org/wiki/EPEL/FAQ#What_is_EPEL.3F) or Extra Packages for Enterprise Linux. These packages are not part of the main distributions but are often used to enhance or extend the functionality of these systems.
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

### Resources
- [Linux Distributions](https://en.wikipedia.org/wiki/List_of_Linux_distributions): A list of all of the different linux distributions.
- [Linux Distribution](https://en.wikipedia.org/wiki/Linux_distribution): In-depth exploration of what a Linux distribution is.
- [Linux Boot Process](https://www.youtube.com/watch?v=XpFsMB6FoOs): High level overview of the Linux boot process.
- [Booting Process of Linux](https://en.wikipedia.org/wiki/Booting_process_of_Linux): In-depth exploration of the Linux boot process.
