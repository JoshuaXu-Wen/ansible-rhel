Role Name
=========

Change Hostname to FQDN

Requirements
------------

``` gather_facts: true ``` in playbook.

Role Variables
--------------

domain_name: dns domain name

Dependencies
------------

None.

Example Playbook
----------------

playbook_rhel_hostname_fqdn.yml

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
