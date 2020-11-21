# Homelab: Proxmox Alpine 3 template

This project builds an Alpine 3 image for Proxmox VE. The cloud-init is installed and configured for further provision by Ansible.

All available parameters can be found at [Proxmox Builder (from an ISO)](https://www.packer.io/docs/builders/proxmox/iso).



# Requirements

- [Packer](https://www.packer.io/)
- A running [Proxmox VE](https://www.proxmox.com/en/proxmox-ve)
- Permissions for creating virtual machines in Proxmox
- The VM should have network access to host which running Packer (8000-9000/tcp).



# Usage

There are several ways for assigning variables.

Environment variables:

```sh
export PROXMOX_API=https://192.168.0.1:8006/api2/json
export PROXMOX_NODE=pve
export PROXMOX_USERNAME=root@pam
export PROXMOX_PASSWORD=secret

packer build alpine.json
```

Packer's variables:

```sh
packer build
    -var proxmox_api=https://192.168.0.1:8006/api2/json \
    -var proxmox_node=pve \
    -var proxmox_username=root@pam \
    -var proxmox_password=secret \
alpine.json
```

External JSON file with variables:

```
# variables.json
{
    "proxmox_api": "https://192.168.0.1:8006/api2/json",
    "proxmox_node": "pve",
    "proxmox_username": "root@pam",
    "proxmox_password": "secret"
}


packer build -var-file variables.json alpine.json
```
