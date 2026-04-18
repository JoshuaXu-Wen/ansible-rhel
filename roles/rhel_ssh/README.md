Role Name
=========

Configure root user authentication, sshd config, banner, motd and pam authentication

Requirements
------------

generate a encrypt root password to replace the default variable root_password

Role Variables
--------------

root_password: encrypt password if required

volumes: list of dict, include the name, size, fs_type and mount_point of LVs.

Dependencies
------------

collections:

- ansible.posix

Example Playbook
----------------

playbook_rhel_ssh.yml

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
