- [Overview](#overview)
- [Project Structure](#project-structure)
- [Usage Guide](#usage-guide)
  - [Installing `kubectl`](#installing-kubectl)


# Overview
This project facilitates the installation of `kubectl` with the latest version on an Ubuntu Desktop (64-bit x86), adhering to [the official instructions](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/).

The process involves downloading the `kubectl` binary, validating it, and then installing it using the `install` command.

* Architecture Support: 64-bit x86 (Intel/AMD).
* Download Source: The latest version of `kubectl` is fetched using a command that retrieves the stable version from [https://cdn.dl.k8s.io/release/stable.txt](https://cdn.dl.k8s.io/release/stable.txt).
* Installation Directory: The binaries are temporarily stored in `/tmp/downloads/` before installation.
* Project Objectives:
  1. To install `kubectl` on an Ubuntu Desktop.

# Project Structure
1. `install_kubectl.yaml`: The main playbook for installing `kubectl`.
2. `inventory`: A file containing details about the master node.

# Usage Guide
## Installing `kubectl`
1. Update the `inventory` file with your specific host configurations.
2. Open a terminal and navigate to the "2-kubectl" directory. 
   1. Verify connectivity to the Ubuntu Desktop with the following command:
    ```bash
    ansible all -i inventory -m ping
    ```
   2. To install `kubectl`, execute:
    ```bash
    ansible-playbook -i inventory install_kubectl.yaml
    ```
    
