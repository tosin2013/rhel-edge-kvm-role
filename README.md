RHEL Edge KVM Deployer role
=========

This role is used to deploy RHEL Edge KVM images that where build from [fleet mananger](https://console.redhat.com/edge/fleet-management).

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

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

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
sudo ansible-playbook  -i hosts runtest.yaml -t create_vm -K


DEstroy a VM
```
sudo ansible-playbook  -i hosts runtest.yaml -t destroy_vm -K
```

License
-------

BSD

Author Information
------------------

Tosin Akinosho
