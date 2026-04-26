Role Name
=========

Register / Unreister client to Satellite / Capsule.
The role have two implementations:

1. use community.general.redhat_subscription module to register host against Satellite/Capsule from target, this is the simple way to register from client
2. However, if the client cannot connect to Satellite directly due to security concerns, use redhat.satellite collection to register the target with deletagation and support granular control (e.g., add host to specific hostgroup )

Recommendation: use the global registation approach for newer version of Satellite.

Requirements
------------

Satellite and Capsules exist in your org.

Role Variables
--------------

activation_key: activation key of repo
capsule_hostname: capsule hostname
capsule_url: capusule URL, if load balancer exist, use the LB url instead.
org_id: organization id of satellite
hostgroup: hostgroup that the host belongs to
location: location of the hostgroup
sat_url: satellite URL
sat_env: location of the satellite
sat_username: satellite registration username
sat_password: satellite registration password

Dependencies
------------

collections:

- community.general
- redhat.satellite

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

