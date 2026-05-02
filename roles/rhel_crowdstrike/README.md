Role Name
=========

Install Crowdstrike

Requirements
------------

collections:

- crowdstrike.falcon

Role Variables
--------------

```
falcon_cid
falcon_apd
falcon_aph
falcon_app
falcon_tags
falcon_message_log
```

Dependencies
------------


Example Playbook
----------------

playbook_rhel_crowdstrike.yml

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

Data: 2/05/2026
