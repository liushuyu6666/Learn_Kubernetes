- [Overview](#overview)
- [Project Structure](#project-structure)
- [Usage Guide](#usage-guide)
  - [Installing and uninstall `etcd`](#installing-and-uninstall-etcd)
  - [Other Operations](#other-operations)
- [Knowledge](#knowledge)
- [Troubleshooting](#troubleshooting)
  - [Device or resource busy:](#device-or-resource-busy)

# Overview
This project installs `etcd` v3.4.16 (with the default `etcdctl`) on an Ubuntu Desktop (64-bit x86) or a Raspberry Pi (64-bit ARM), following the official [v3.4.16 release instructions](https://github.com/etcd-io/etcd/releases/tag/v3.4.16). Please note that this project may require updates for newer release versions.

After downloading and extracting the binary, `etcd` will be integrated with `systemd` for management.

* Architecture: 64-bit x86 (Intel/AMD) or 64-bit ARM.
* Download Source: [https://storage.googleapis.com/etcd](https://storage.googleapis.com/etcd)
* Release Version: v3.4.16
* Installation Directory: `/tmp/etcd-download-test/`
* This project aims to achieve the following objectives:
  1. Check the configuration and connection in the cluster.
  2. Gain insights into the distinctions between `amd64` and `arm64` for Kubernetes installation and management.
  3. Develop proficiency in utilizing `systemd`.
  4. Acquire foundational knowledge of Ansible.
  5. Troubleshoot some potential issues.

# Project Structure
1. `subtasks/`: This directory contains subtasks that are included in the main playbooks.
   1. `import_configs.yaml`: Imports configurations and determines the architecture type.
   2. `clean_up.yaml`: Performs clean-up tasks to remove any remnants.
2. `install_etcd`: The main entry point for the installation of `etcd`.
3. `uninstall_etcd`: The main entry point for uninstalling `etcd`.
4. `inventory`: Contains information about hosts and their configurations.
5. `template/`: Stores templates.
   1. `etcd.service.j2`: A Jinja2 template for the `etcd.service` file used with `systemd` for managing the `etcd` service.
6. `config.example.yaml` and `config.yaml`: These files store configuration details, including credentials, for your project. `config.example.yaml` is typically used as a template or reference, while `config.yaml` contains the actual configuration.

# Usage Guide
## Installing and uninstall `etcd`
1. Setup SSH connections as instructed in the "readme" file.
2. Update `inventory` with your specific configurations (e.g., `ansible_host`, `ansible_ssh_user`, `ansible_ssh_private_key_file`).
3. Duplicate `config.example.yaml` and rename the copy file to `config.yaml`. 
   1. Visit the [official etcd releases page](https://github.com/etcd-io/etcd/releases) to find the latest release version. If needed, update specific configurations, such as `etcd_version` and `download_url`, in the `config.yaml` file.
4. Open the terminal and then navigate to the "1-start" folder.
   1. Check the connectivity to the Ubuntu Desktop using the following command:
    ```bash
    ansible all -i inventory -m ping
    ```
   2. Modify the `hosts` entry in the `install_etcd.yaml` or `uninstall_etcd.yaml` file to specify the device on which you wish to install or uninstall `etcd`.
   3. Install `etcd` by running:
    ```bash
    ansible-playbook -i inventory install_etcd.yaml
    ```
   4. Uninstall `etcd` by running:
    ```bash
    ansible-playbook -i inventory uninstall_etcd.yaml
    ```

## Other Operations
1. Interact with `etcd` using `etcdctl`:
You can use `etcdctl` to interact with the `etcd` key-value store. The basic syntax is as follows:
```bash
/tmp/etcd-download-test/etcdctl --endpoints=localhost:2379 <command>
```
Here are some examples of common operations:
   * To check the `etcd` version:
    ```bash
    /tmp/etcd-download-test/etcdctl --endpoints=localhost:2379 version
    ```
   * To insert a key-value pair:
    ```bash
    /tmp/etcd-download-test/etcdctl --endpoints=localhost:2379 put key value
    ```
   * To list all key-value pairs:
    ```bash
    /tmp/etcd-download-test/etcdctl --endpoints=localhost:2379 get --prefix ""
    ```
2. Checking `etcd` Port and PID:
If you need to verify the etcd process by its port, you can use the following command to check the PID:
```bash
sudo lsof -n -i :2379
```
This command will display the PID associated with the `etcd` process listening on port 2379.


# Knowledge
1. When installing `etcd`, it includes both the `etcdctl` client and a gRPC API. The gRPC API serves as the communication interface for interactions between clients and the `etcd` server.
2. Integrate `etcd` with `systemd` by creating an 'etcd.service' file in the '/etc/systemd/system/' directory. Remember to reload 'systemd' afterward.

# Troubleshooting
## Device or resource busy:
When encountering the 'Error loading unit file 'etcd': System.Error.EBUSY' on Raspberry Pi, follow these steps to resolve the issue:
1. Update the `etcd.service` template with the following lines to prevent the error:
```bash
[Service]
ExecStart=/tmp/etcd-download-test/etcd
Restart=on-failure
RestartSec=5
Environment=ETCD_UNSUPPORTED_ARCH=arm64
```
   * `Restart=on-failure` specifies that the service should be restarted only if it exits with a non-zero status code, indicating a failure. It doesn't restart on normal, clean exits (status code 0).
   * `RestartSec=5` sets a delay of 5 seconds between service restarts. If the service fails and `Restart=on-failure` is triggered, it waits for 5 seconds before attempting to restart the service. This can prevent rapid restart loops in case of a failure.
   * `Restart=always` specifies that the service should be restarted regardless of the exit status. Whether the service exits with a success (status code 0) or failure (non-zero status code), it will be restarted.

1. Reload `systemd` to apply the changes:
```bash
sudo systemctl daemon-reload
```