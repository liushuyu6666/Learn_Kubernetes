- [Overview](#overview)
  - [Project Structure](#project-structure)
- [Usage Guide](#usage-guide)
  - [Installing and uninstall `etcd`](#installing-and-uninstall-etcd)
  - [Other Operations](#other-operations)
- [Knowledge](#knowledge)
- [TODO](#todo)

# Overview
This project installs `etcd` v3.4.16 (with the default `etcdctl`) on an Ubuntu Desktop (64-bit x86) or a Raspberry Pi (64-bit ARM), following the official [v3.4.16 release instructions](https://github.com/etcd-io/etcd/releases/tag/v3.4.16). Please note that this project may require updates for newer release versions.

* Architecture: 64-bit x86 (Intel/AMD) or 64-bit ARM.
* Download Source: [https://storage.googleapis.com/etcd](https://storage.googleapis.com/etcd)
* Release Version: v3.4.16
* Installation Directory: `/tmp/etcd-download-test/`

After downloading and extracting the binary, `etcd` will be integrated with `systemd` for management.

## Project Structure
1. `subtasks/`: This directory contains subtasks that are included in the main playbooks.
   1. `import_configs.yaml`: Imports configurations and determines the architecture type.
   2. `clean_up.yaml`: Performs clean-up tasks to remove any remnants.
2. `install_etcd`: The main entry point for the installation of `etcd`.
3. `uninstall_etcd`: The main entry point for uninstalling `etcd`.
4. `inventory`: Contains information about hosts and their configurations.
5. `etcd.service.j2`: A Jinja2 template for the `etcd.service` file used with `systemd` for managing the `etcd` service.
6. `config.example.yaml` and `config.yaml`: These files store configuration details, including credentials, for your project. `config.example.yaml` is typically used as a template or reference, while `config.yaml` contains the actual configuration.

# Usage Guide
## Installing and uninstall `etcd`
1. Setup SSH connections as instructed in the "readme" file.
2. Update `inventory` with your specific configurations (e.g., `ansible_host`, `ansible_ssh_user`, `ansible_ssh_private_key_file`).
3. Duplicate `config.example.yaml` and rename the copy file to `config.yaml`. 
   1. Visit the [official etcd releases page](https://github.com/etcd-io/etcd/releases) to find the latest release version. If needed, update specific configurations, such as `etcd_version` and `download_url`, in the `config.yaml` file.
4. Navigate to the "project1" folder.
   1. Check the connectivity to the Ubuntu Desktop using the following command:
    ```bash
    ansible all -i inventory -m ping
    ```
   2. Change `hosts` on `install_etcd.yaml` or `uninstall_etcd.yaml` file.
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
When install `etcd`, both `etcdctl` client and a gRPC API are installed. The gRPC API is used by `etcd` for its communication between clients and the `etcd` server.

# TODO
`sudo systemctl start etcd` cannot work on Raspberry Pi