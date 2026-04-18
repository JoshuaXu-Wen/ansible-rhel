Role Name
=========

Register NTP servers

Requirements
------------

NTP Servers exist in your org.

Role Variables
--------------

ntp_server1:
ntp_server2:
...

Dependencies
------------

roles:
- redhat.rhel_system_roles

Example Playbook
----------------

playbook_rhel_ntp.yml

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
