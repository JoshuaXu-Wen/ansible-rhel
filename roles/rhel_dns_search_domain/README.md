Role Name
=========

Configure DNS search domains

Requirements
------------

None.

Role Variables
--------------

dns_search_domains: List of dns domains, seperate with comma

Dependencies
------------

None.

Example Playbook
----------------

playbook_rhel_dns_search_domain.yml

Test
----------------

ansible-navigator run tests/test.yml -i tests/inventory

Execution Environment
----------------

registry.redhat.io/ansible-automation-platform-25/ee-supported-rhel9:latest

Reference
----------------

https://learn.microsoft.com/en-us/troubleshoot/azure/virtual-machines/linux/custom-dns-configuration-for-azure-linux-vms?tabs=RHEL

License
-------

MIT

Author Information
------------------

Name: Joshua Xu

Email: manmandes10010@gmail.com

Data: 18/04/2026
