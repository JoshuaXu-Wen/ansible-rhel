Role Name
=========

RHEL OS disk (LVM) partition.

Requirements
------------

The role will need to install utility tools like gdisk, so the satellite registration is required as pre-requisite.

Role Variables
--------------

fs_type: filesystem, options: xfs or ext4

volumes: list of dict, include the name, size, fs_type and mount_point of LVs.

Dependencies
------------

roles:

- redhat.rhel_system_roles

- rhel_rhsm

Example Playbook
----------------

playbook_rhel_os_partition.yml

Test
----------------

ansible-navigator run tests/test.yml -i tests/inventory

Execution Environment
----------------

registry.redhat.io/ansible-automation-platform-25/ee-supported-rhel9:latest

License
-------

MIT

Author Information
------------------

Name: Joshua Xu

Email: manmandes10010@gmail.com

Data: 18/04/2026
