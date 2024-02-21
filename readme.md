- [Overview](#overview)
- [How to use](#how-to-use)
  - [Setting Up SSH Access](#setting-up-ssh-access)
    - [Ubuntu Desktop Configuration](#ubuntu-desktop-configuration)
    - [Raspberry Pi Setup Guide](#raspberry-pi-setup-guide)
  - [Setting Up Ansible](#setting-up-ansible)
- [Projects overview](#projects-overview)
  - [Project 1](#project-1)
- [References](#references)

# Overview
This project is aimed at practical Kubernetes learning. It involves the utilization of a single Ubuntu Desktop (64-bit) laptop as the master node and three Raspberry Pi devices running Ubuntu Server (64-bit) as worker nodes. Additionally, a MacBook is required for remote control and configuration of both the master node (Ubuntu Desktop) and the worker nodes (Raspberry Pi).

For effective management, SSH access is established from the MacBook to both the master and worker nodes.

Checklist:
1. MacBook x1 (to control both master and worker nodes); Architecture: 64-bit x86 (Intel/AMD).
2. Ubuntu Desktop x1 (master node). user: 'ubuntu_desktop'; Architecture: ARM 64-bit.
3. Raspberry Pi x3 (worker node). user: 'raspberrypi1', 'raspberrypi2' and 'raspberrypi3'.

# How to use
## Setting Up SSH Access
### Ubuntu Desktop Configuration
For SSH access from the MacBook to the Ubuntu Desktop (master nodes) for controlling and configuring, please refer to the provided [instructions](https://github.com/liushuyu6666/Knowledge/blob/master/Networking/SSH.md#practice). Ensure that the username on the Ubuntu Desktop is set to 'ubuntu_desktop'.

### Raspberry Pi Setup Guide
For SSH access from the MacBook to the Raspberry Pi devices (worker nodes) to control and configure them, please follow the instructions provided [here](https://liushuyu.atlassian.net/wiki/spaces/TECHHOME/pages/86343683/Setup). Ensure that the username on three Raspberry Pi devices should be 'raspberrypi1', 'raspberrypi2' and 'raspberrypi3'.

## Setting Up Ansible
Ansible should be installed on the MacBook; there's no need to install it on the Raspberry Pi or the Ubuntu Desktop laptop.

# Projects overview
## Project 1
* `64-bit x86`
* `64-bit ARM`
* `systemd`
* Ansible
* `etcd`

# References
1. [Kubernetes the Hard Way Raspberry Pi](https://github.com/robertojrojas/kubernetes-the-hard-way-raspberry-pi)