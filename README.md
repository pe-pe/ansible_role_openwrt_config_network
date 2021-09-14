OpenWRT Config Network
=========

[![Role](https://img.shields.io/ansible/role/56237.svg)](https://galaxy.ansible.com/pe_pe/openwrt_config_network/)
[![Quality](https://img.shields.io/ansible/quality/56237.svg)](https://galaxy.ansible.com/pe_pe/openwrt_config_network/)
[![CI](https://github.com/pe-pe/ansible_role_openwrt_config_network/workflows/CI/badge.svg)](https://github.com/pe-pe/ansible_role_openwrt_config_network/actions)

Ansible role that configures network settings of OpenWRT device (mainly those which are usually defined in `/etc/config/network`).

Requirements
------------
None

Role variables
--------------
Configuration settings defined in `openwrt_config_network` variable which are to be applied on OpenWRT device.
```yaml
openwrt_config_network:
  globals:
    ula_prefix: "fd27:70fa:5c1d::/48"
  interfaces:
    lan: { ifname: eth1 }
    xlan: { proto: static, ipaddr: 192.168.255.254, netmask: 255.255.255.0, gateway: 192.168.255.1, dns: [192.168.255.2] }
```
If `openwrt_config_network` configuration variable is not present - no changes are made by role.

Dependencies
------------
This role depends on Ansible role `gekmihesg.openwrt` which allows to manage OpenWRT and derivatives with Ansible but without Python.

Example playbook using the role
-------------------------------
`./host_vars` \
`./host_vars/myrouter.yml`
```yaml
---
openwrt_config_network:
  globals:
    ula_prefix: "fd27:70fa:5c1d::/48"
  interfaces:
    lan: { ifname: eth1 }
    xlan: { proto: static, ipaddr: 192.168.255.254, netmask: 255.255.255.0, gateway: 192.168.255.1, dns: [192.168.255.2] }
```
`./inventory.ini`
```ini
[openwrt]
myrouter
```
`./roles` \
`./roles/requirements.yml`
```yaml
---
roles:
- name: gekmihesg.openwrt
- name: pe_pe.openwrt_config_network
```
`./site.yml`
```yaml
---
- hosts: all
  roles:
    - role: gekmihesg.openwrt
    - role: pe_pe.openwrt_config_network
```
`./ansible.cfg`
```ini
[defaults]
# Define inventory location
inventory = ./inventory.ini
# Where to put roles downloaded from galaxy and other repos
roles_path = ./roles
# Defaults to /tmp to avoid flash wear on target device
remote_tmp = /tmp
```

Example execution
-----------------
Install roles and requirements:
```
ansible-galaxy role install -r roles/requirements.yml
```
Preview changes execution would perform on inventory:
```
ansible-playbook site.yml --check --diff
```
Execute playbook on inventory:
```
ansible-playbook site.yml
```
License
-------
MIT

Author Information
------------------
PePe
