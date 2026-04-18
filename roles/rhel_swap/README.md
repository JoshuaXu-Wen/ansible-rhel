Role Name
=========

rhel_swap:

Integrate Swap patition into image.

Requirements
------------

None

Role Variables
--------------

cloud_cfg_file: cloud init file path.

Dependencies
------------

None.

Example Playbook
----------------

playbook_rhel_swap.yml

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
