# Using Salt

*Introduction to SaltStack, a Linux configuration managment tool.*

---

## What is Salt?
**Salt,** also called **SaltStack,** is an open-source configuration managment and automation tool. It allows system administrators to:
- Define system states (e.g. install packages, run services, configure users, etc.)
- Apply those configurations across multiple machines consistently
- Automate routine infrastructure tasks like updates, configuration changes, or user provisioning

Salt follows a master-minion architecture, where:
- The Salt master sends commands and configurations
- The Salt minion executes those commands

A deeper introduction to **Salt** can be found [here](https://docs.saltproject.io/en/3006/topics/index.html).

## Installing Salt
The Salt Project documentation offers a [quick installation guide](https://docs.saltproject.io/salt/install-guide/en/latest/index.html) for Linux based operating systems. If you are running RHEL-like systems, follow the [Linux (RPM) Install Guide](https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-rpm.html). If you are running Debian-like systems, follow the [Linux (DEB) Install Guide](https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html). Each guide includes post-installation steps for configuring the Salt master and minions, starting the master and minion services, accepting the minion keys, and verifying your Salt installation. 

## Understanding Salt
As previously mentioned, Salt is a powerful open-source tool for automating system configuration, remote execution, and infrastrcuture management. It uses a master/minion model where the master controls and sends instructions and the minion recieves and applies configurations. There are several key concepts that will be important to know when working with Salt.

### Key Concepts
|**Concept**|**Description**                   |
|:---------:|:---------------------------------|
|  State    | A YAML file that describes the desired configuration of a system.|
|  Grains   | Static system facts collected by the minion (like OS, IP, CPU type). Can be used to target systems based on their characteristics.|
|  Pillar   | Secure targeted data defined on the master and passed to the minions. Used for secrets, config values, or variables in state files.|
| Top File  | A special file `top.sls` that tells Salt which states to apply to which minions. It acts as the entry point for configuration.|
| Highstate | The process of applying all states defined in the top file to the appropriate minions.|
| Formulas  | Reusable Salt state modules that configure common components (like users or services).|

### Common Salt Commands
|**Command**|**Description**|
|:------------------:|:---------------|
|`salt '*' test.ping`|Ping all minions|
|`salt '*' grains.item host`|Get minion hostname|
|`salt '*' grains.item`|Get full grain info|
|`salt '*' grains.item os osrelease`|Get OS details|
|`salt '*' cmd.run 'uptime'`|Run a shell command on minions|
|`salt '*' state.apply myfile`|Apply a file to a state|
|`salt '*' state.apply`|Run highstate|

## Using Vagrant as a Development Environment (optional)
[Vagrant](https://developer.hashicorp.com/vagrant) is a tool for managing virtual machine environments in a reproducible way using simple configuration files called `Vagrantfile`. Vagrant makes it easy to rebuild development environments, which is great for testing Salt states before applying them in production. Vagrant is also compatible with KVM environments. Learn more about using Vagrant with your KVM / Libvirt environment [here](https://github.com/vagrant-libvirt/vagrant-libvirt). 

## Resources
- [Salt Installation Guide](https://docs.saltproject.io/salt/install-guide/en/latest/index.html): Instructions for installing Salt
- [SaltStack Installation Tutorial](https://www.tutorialspoint.com/saltstack/saltstack_installation.htm): Ubuntu based Salt intallation tutorial
- [Salt in 10 Minutes](https://docs.saltproject.io/en/latest/topics/tutorials/walkthrough.html): A quick guide to understanding Salt
- [Creating a Simple Environment](https://www.tutorialspoint.com/saltstack/saltstack_creating_simple_environment.htm): Tutorial using Vagrant to create a simple demo environment
- [Vagrant Documentation](https://developer.hashicorp.com/vagrant): Offical Vagrant documentation site
- [Installing Vagrant](https://developer.hashicorp.com/vagrant/install): Basic steps to get Vagrant installed in your environment
- [Using Vagrant with KVM/Libvirt](https://github.com/vagrant-libvirt/vagrant-libvirt): A Vagrant plugin that adds a Libvirt provider to Vagrant
- [Salt Overview](https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html): Deep dive into Salt's architecture
- [Salt Grains](https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html): Deep explanation of Salt grains
- [Salt States](https://docs.saltproject.io/salt/user-guide/en/latest/topics/states.html): Deep explanation of Salt states
- [Salt Pillar](https://docs.saltproject.io/salt/user-guide/en/latest/topics/pillar.html): Deep explanation of Salt pillar data
- [Salt Formulas](https://docs.saltproject.io/en/3006/topics/development/conventions/formulas.html): Deep explanation of Salt formulas
- [How to Create Your First Salt Formula](https://www.digitalocean.com/community/tutorials/how-to-create-your-first-salt-formula): A tutorial to create your first Salt formula
- [Saltstack Cheatsheet](https://github.com/harkx/saltstack-cheatsheet?tab=readme-ov-file): Collection of commonly used commands.
