- [Overview](#overview)
- [Usage Guide](#usage-guide)
  - [Installing `etcd` on Ubuntu Desktop](#installing-etcd-on-ubuntu-desktop)

# Overview
This project installs `etcd` v3.4.16 on an Ubuntu Desktop, following the official [v3.4.16 release instructions](https://github.com/etcd-io/etcd/releases/tag/v3.4.16). Please note that this project may require updates for newer release versions.

Download Source: [https://storage.googleapis.com/etcd](https://storage.googleapis.com/etcd)
Release Version: v3.4.16
Installation Directory: `/tmp/etcd-download-test/`

After downloading and extracting the binary, etcd will be integrated with systemd for management.

# Usage Guide
## Installing `etcd` on Ubuntu Desktop
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

