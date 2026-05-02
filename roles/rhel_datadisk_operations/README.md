Role Name
=========

RHEL Data disk operations:

1. add adn mount new data disk
2. remount data disk
3. remove data disk

Requirements
------------

None.

Role Variables
--------------

operation_name:
mount_point:
disk_name:
fs_type:
...

Dependencies
------------

Example Playbook
----------------

playbook_rhel_datadisk_operations.yml

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

Data: 1/05/2026
