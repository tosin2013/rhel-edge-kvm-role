RHEL Edge KVM Deployer role
=========

This role is used to deploy RHEL Edge KVM images that where build from [fleet mananger](https://console.redhat.com/edge/fleet-management).


[![ansible-lint](https://github.com/tosin2013/rhel-edge-kvm-role/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/tosin2013/rhel-edge-kvm-role/actions/workflows/ansible-lint.yml)

Requirements
------------

* Ansible 2.9 or higher
```
ansible-galaxy collection install community.libvirt
ansible-galaxy collection install ansible.posix
ansible-galaxy collection install community.general
```

* NMAP
```
sudo yum install nmap -y
```

Role Variables
--------------

```

libvirt_image_dir: /var/lib/libvirt/images
libvirt_iso_dir:  /var/lib/libvirt/images
libvirt_iso_name: rhel-edge-kvm.iso
libvirt_vm_name:  rhel-edge-kvm
template_dir: /tmp/
libvirt_defaults:
  edge_device:
    cpu: 2
    memory: 2097152 

virtual_machines:
  - name: "{{ libvirt_vm_name }}"
    hostname: "{{ libvirt_vm_name }}" # there is a character limit with the hostname it will brake sysprep
    password: "{{ libvirt_vm_name }}"
    os: "rhel85"
    isos:
      - name: "{{ libvirt_iso_name }}"
        dev: sdb
    disk_size: 20G
    image_index: 2
    image_name: "RHEL Edge image"
    disk_iso: "{{ libvirt_vm_name }}"
    connection_type: "bridge" # "bridge" or "network" bridge is default
    bridgename: "provisioning" 
    bridge_mac: "{{ '52:54:00' | community.general.random_mac }}"
    vlanid: 0 # use 503 in network mode for emulated lab or 0 in hardware bridge mode
    subnet: "192.168.1.1/24"
    secondary_dns: 1.1.1.1
```

Dependencies
------------

* Ansible 2.9 or higher
```
sudo ansible-galaxy install git+https://github.com/tosin2013/rhel-edge-kvm-role.git --force
```

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    cat edge_vm.yml
    - hosts: client
      roles:
        - rhel-edge-kvm-role

    cat hosts
    [client]
    localhost   ansible_connection=local

CREATE A VM
```
sudo ansible-playbook  -i hosts edge_vm.yml -t create_kvm_vm -K
```

Destroy a VM
```
sudo ansible-playbook  -i hosts edge_vm.yml -t destroy_kvm_vm -K
```

License
-------

BSD

Author Information
------------------

Tosin Akinosho
