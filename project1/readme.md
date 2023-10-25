- [Overview](#overview)
- [Usage Guide](#usage-guide)
  - [Installing and uninstall `etcd` on Ubuntu Desktop](#installing-and-uninstall-etcd-on-ubuntu-desktop)
  - [Other Operations](#other-operations)

# Overview
This project installs `etcd` v3.4.16 (with the default `etcdctl`) on an Ubuntu Desktop separately, following the official [v3.4.16 release instructions](https://github.com/etcd-io/etcd/releases/tag/v3.4.16). Please note that this project may require updates for newer release versions.

* Download Source: [https://storage.googleapis.com/etcd](https://storage.googleapis.com/etcd)
* Release Version: v3.4.16
* Installation Directory: `/tmp/etcd-download-test/`

After downloading and extracting the binary, etcd will be integrated with systemd for management.

# Usage Guide
## Installing and uninstall `etcd` on Ubuntu Desktop
1. Setup SSH connections as instructed in the "readme" file.
2. Update `inventory` with your specific configurations (e.g., `ansible_host`, `ansible_ssh_user`, `ansible_ssh_private_key_file`).
3. Duplicate `config.example.yaml` and rename the copy file to `config.yaml`. 
   1. Visit the [official etcd releases page](https://github.com/etcd-io/etcd/releases) to find the latest release version. If needed, update specific configurations, such as `etcd_version` and `download_url`, in the `config.yaml` file.
4. Navigate to the "project1" folder.
   1. Check the connectivity to the Ubuntu Desktop using the following command:
    ```bash
    ansible all -i inventory -m ping
    ```
   2. Install `etcd` on Ubuntu Desktop by running:
    ```bash
    ansible-playbook -i inventory install_etcd.yaml
    ```
   3. Uninstall `etcd` by running:
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