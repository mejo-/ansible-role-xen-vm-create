# Ansible role to create VMs on a Xen Dom0

[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-xen-vm-create-blue.svg)](https://galaxy.ansible.com/mejo-/xen-vm-create/)

This role creates a Xen VM on a Dom0. It requires several variables
to be set (see below).

# How it works

The role is meant to be executed from an Ansible script. The following
script is an example:

```
# Usage:
#   ansible-playbook scripts/xen_vm_create.yml -e "<VARIABLES>"
#
# Supported variables:
#   * vm_name:     name of the VM
#   * lvm_vg:      LVM volume group holding Xen VM volumes (optional, default 'vgxen')
#   * diskingb:    harddisk size in GB
#   * meminmb:     memory size in MB
#   * cpus:        pattern for CPU cores to be used (optional)
#   * vcpus:       number of VCPUs to be assigned (optional, default 2)
#   * release:     name of the Debian release (currently supported: jessie, stretch)
#   * ip:          IP address of the VM
#   * mac:         MAC address (optional, auto-generated by default)
#   * netmask:     network netmask
#   * gateway:     network gateway
#   * nameservers: nameservers
#   * xenbr:       name of the xen bridge
#   * preseed:     name of the preseed to be used (optional, default 'vm-preseed')
#   * auto:        start automatically at hypervisor boot (optional, default 'yes')
#
# Example:
#   ansible-playbook scripts/xen_vm_create.yml -e "vm_name=<vm-name> diskingb=5 meminmb=2048 ip=192.168.1.2"
#
# 1. Add new VM to the Ansible inventory file
# 2. Run the script like in example above 

- hosts: <xen-dom0>
  roles:
    - xen-vm-create
  tags:
    - xen-vm-create
  vars:
    release: stretch
    lvm_vg: vgxen
    netmask: 255.255.255.0
    gateway: 192.168.1.1
    nameservers:
      - 194.150.168.168 
    xenbr: xenbr0
    preseed: vm-preseed
```

This script can be executed according to the docs in it.

# Defaults

```
xen_preseed_urlbase:
```

# License

This Ansible role is licensed under the GNU GPLv3 or later.

# Author

Copyright 2017 Jonas Meurer <jonas@freesources.org>
