# Using Ansible

*Introduction to Ansible, an open-source automation tool for configuration management.*

---

## What is Ansible?
**Ansible** is an open-source automation tool used to configure systems, deploy software, and orchestrate advanced workflows like application deployment and system updates. It allows system administrators to manage systems at scale without having to manually log into each machine. Unlike Salt, Ansible is agentless and uses SSH to connect to remote systems and execute tasks.

### Key Concepts
|**Concept**|**Description**|
|:---------:|:--------------|
|Control Node|The machine which you run Ansible CLI tools.|
|Managed Nodes|Also referred to as "hosts", these are the systems that ansible connects to and configures.|
|Inventory|A list of hosts (and groups of hosts) that Ansible manages. Defined in a file called `hosts`.|
|Playbook|A YAML file that defines the desired state of one or more systems through "plays" and "tasks".|
|Module|Small programs that perform specific tasks (install a package, copy a file, start a service).|
|Task|A single action defined in a playbook.|
|Role|A structured way to organize playbooks and reuseable automation code.|

### How Does Ansible Work?

1. Inventory deines what systems to manage.
2. Playbooks define what actions to take.
3. Ansible connects to each system via SSH using the credentials provided.
4. Tasks are executed through modules.
5. The results are reported back in the terminal.

## Using Vagrant as a Development Environment
[Vagrant](https://developer.hashicorp.com/vagrant) is a tool for managing virtual machine environments in a reproducible way using simple configuration files called `Vagrantfile`. Vagrant makes it easy to rebuild development environments, which is great for testing Salt states before applying them in production. Vagrant is also compatible with KVM environments. Learn more about using Vagrant with your KVM / Libvirt environment [here](https://github.com/vagrant-libvirt/vagrant-libvirt).

### Ansible Lab using Vagrant

[Ansible Lab](https://github.com/chloegerhardson/ansible_lab): This repository builds an ansible lab environment using Vagrant and Libvirt to create a small cluster of virtual machines for running playbooks, configuration management, and orchestration exercises.

---

## Resources
- [Ansible Docs](https://docs.ansible.com/ansible/latest/getting_started/index.html): Getting started with Ansible
- [Ansible Lab](https://github.com/chloegerhardson/ansible_lab): Ansible Lab sandbox environment
- [Vagrant Documentation](https://developer.hashicorp.com/vagrant): Offical Vagrant documentation site
- [Installing Vagrant](https://developer.hashicorp.com/vagrant/install): Basic steps to get Vagrant installed in your environment
- [Using Vagrant with KVM/Libvirt](https://github.com/vagrant-libvirt/vagrant-libvirt): A Vagrant plugin that adds a Libvirt provider to Vagrant
- [Ansible Tutorial for Beginners](https://spacelift.io/blog/ansible-tutorial): Beginner tutorial using Vagrant and Virtual Box
