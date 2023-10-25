- [Overview](#overview)
- [How to use](#how-to-use)
  - [Setting Up SSH Access](#setting-up-ssh-access)
    - [Ubuntu Desktop Configuration](#ubuntu-desktop-configuration)
    - [Raspberry Pi Setup Guide](#raspberry-pi-setup-guide)

# Overview
This project is aimed at practical Kubernetes learning. It involves the utilization of a single Ubuntu Desktop (64-bit) laptop as the master node and three Raspberry Pi devices running Ubuntu Server (64-bit) as worker nodes. Additionally, a MacBook is required for remote control and configuration of both the master node (Ubuntu Desktop) and the worker nodes (Raspberry Pi).

For effective management, SSH access is established from the MacBook to both the master and worker nodes.

Checklist:
1. MacBook x1 (to control both master and worker nodes)
2. Ubuntu Desktop x1 (master node). user: 'ubuntu_desktop'.
3. Raspberry Pi x3 (worker node). user: 'raspberrypi1', 'raspberrypi2' and 'raspberrypi3'.

# How to use
## Setting Up SSH Access
### Ubuntu Desktop Configuration
For SSH access from the MacBook to the Ubuntu Desktop (master nodes) for controlling and configuring, please refer to the provided [instructions](https://github.com/liushuyu6666/Knowledge/blob/master/Networking/SSH.md#practice). Ensure that the username on the Ubuntu Desktop is set to 'ubuntu_desktop'.

### Raspberry Pi Setup Guide
For SSH access from the MacBook to the Raspberry Pi devices (worker nodes) to control and configure them, please follow the instructions provided [here](https://github.com/liushuyu6666/Learn_Ansible/blob/master/readme.md#raspberry-pi-setup-guide). Ensure that the username on three Raspberry Pi devices should be 'raspberrypi1', 'raspberrypi2' and 'raspberrypi3'.