Bootstrap Swarm Project 
=============================

<img src="./bootstrap-swarm-project.webp" alt="Bootstrap Swarm Project" width="200" height="200">

# Description

This Ansible playbook initializes a Docker Swarm cluster on a group of Raspberry Pi devices. It includes roles for system updates, Docker installation, system configuration, and Swarm cluster initialization. 

# Installation

To use this playbook, ensure Ansible is installed on your machine. For macOS, you can install Ansible using Homebrew:
```
brew install ansible
```
Alternatively, for other platforms, install via `pip`:
```
pip install ansible
```

Once Ansible is installed, clone this repository and run the playbook with the following command:
```
ansible-playbook -i <inventory_file> playbooks/main.yml
```
Replace `<inventory_file>` with the path to your Ansible inventory file, which should contain the list of hosts for your Swarm cluster.

# Basic Usage

Simply run the playbook using the command above, specifying the hosts you want to include in your Swarm cluster. The playbook will handle updating the system, installing Docker, configuring the system, and initializing the Swarm cluster.

Example:
```
ansible-playbook -i inventory playbooks/main.yml
```
This will execute the playbook on all hosts listed in the `inventory` file.

## Advanced Usage

### Customizing Message Of The Day (MOTD)

You can create a custom message of the day (MOTD), which appears when logging into your system. Update the this [MOTD](playbooks/roles/ansible-role-system-configuration/files/motd) role's variables to define your MOTD message.

### Using Docker Visualizer

The `swarm-initialization` role includes a step to create a Docker service running Docker Visualizer, which is published on port 8080.

# Ansible roles

## [ansible-role-python-raspbian-bootstrap](playbooks/roles/ansible-role-python-raspbian-bootstrap/)

Bootstraps a Raspbian system with Python and essential packages.

Features:

- Updates the package list.
- Installs Python and pip.
- Installs essential Python packages.

## [ansible-role-system-upgrade](playbooks/roles/ansible-role-system-upgrade/)

Upgrades system packages to their latest versions.

Features:

Features:
- Updates the package list.
- Upgrades all installed packages.
- Optionally reboots the system if required.

## [ansible-role-install-docker](playbooks/roles/ansible-role-install-docker/)

Installs and configures Docker on a target system.

Features:
- Downloads and runs the Docker installation script.
- Adds the current user to the Docker group.
- Configures Docker to start with systemd.
- Sets up Docker daemon configuration.

## [ansible-role-system-configuration](playbooks/roles/ansible-role-system-configuration/)

Configures various system settings on a target host.

Features:
- Configures system timezone.
- Sets up hostname and hosts file.
- Manages user accounts and groups.
- Configures SSH settings.

## [ansible-role-swarm-initialization](playbooks/roles/ansible-role-swarm-initialization/)

Initializes a Docker Swarm on a target host.

Features:
- Initializes a Docker Swarm on the nodes.
- Manages invitations for managers and workers to join the Swarm.
- Configures Docker Swarm settings.
- Creates a Docker Visualizer service.

# License
GPLv3