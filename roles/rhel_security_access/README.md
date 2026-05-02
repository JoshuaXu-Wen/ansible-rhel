Role Name
=========

1. Remove Azure inital local admin account
2. Add AD group into local admin

Requirements
------------

host is machine joined

None.

Role Variables
--------------

default_admin_user: admin
domain_user_groups: []
...

Dependencies
------------

roles:

- redhat.rhel_system_roles.ad_integration

Example Playbook
----------------

playbook_rhel_security_access.yml

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
