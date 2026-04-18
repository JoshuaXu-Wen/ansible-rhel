Role Name
=========

Install minimal-environment packages, AD and dnf version lock in Golden Image.

Requirements
------------

RHEL subscription registered

Role Variables
--------------

None.

Dependencies
------------

None


Example Playbook
----------------

playbook_rhel_package_install.yml

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
