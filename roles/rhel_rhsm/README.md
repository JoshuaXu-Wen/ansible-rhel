Role Name
=========

Register / Unreister client to Satellite / Capsule.

Requirements
------------

Satellite and Capsules exist in your org.

Role Variables
--------------

activation_key: activation key of repo
capsule_hostname: capsule hostname
capsule_url: capusule URL, if load balancer exist, use the LB url instead.
org_id: organization id of satellite
sat_env: location of the satellite
sat_username: satellite registration username
sat_password: satellite registration password

Dependencies
------------

collections:
- community.general

Example Playbook
----------------

playbook_rhel_rhsm.yml

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

