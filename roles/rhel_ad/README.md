Role Name
=========

Register Host to AD Domain

Requirements
------------

None.

Role Variables
--------------

domain_user:
domain_password:
domain_realm:
domain_ou:
allow_rc4_crypto
ntp_server:
...

Dependencies
------------

Example Playbook
----------------

playbook_rhel_ad.yml

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
