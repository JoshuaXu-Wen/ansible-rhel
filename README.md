# ansible-rhel

Ansible roles and playbooks for RHEL image automation.

This repository builds a reusable and hardened RHEL image baseline using `playbook_rhel_image_build.yml`.

## Playbook flow (`playbook_rhel_image_build.yml`)

1. Set SELinux to permissive during build.
2. Set persistent hostname to FQDN (`rhel_hostname_fqdn`).
3. Configure DNS search list for DHCP client (`rhel_dns_search_domain`).
4. Recollect ansible fact after hostname change.
5. Register host to Satellite/Capsule (`rhel_rhsm`).
6. Resize OS partition and apply LVM layout (`rhel_os_partition`).
7. Install base packages (`rhel_package_install`).
8. Update all packages to latest (`dnf name="*" state=latest`).
9. Apply baseline OS settings (`rhel_basic_config`).
10. Configure NTP/chrony (`rhel_ntp`).
11. Configure log rotation and rsyslog (`rhel_logrotation`).
12. Apply SSH hardening, keys, and optional PAM setup (`rhel_ssh`).
13. Configure Azure swap behavior via cloud-init (`rhel_swap`).
14. Remove transient/sensitive artifacts (`rhel_cleanup`).
15. Unregister from Satellite/Capsule (`rhel_rhsm`, `unregister.yml`).
16. Set SELinux back to enforcing.

## Roles: responsibilities and variables

### `rhel_hostname_fqdn`

Responsibilities:

- Set the persistent hostname to `{{ inventory_hostname }}.{{ domain_name }}` (systemd).
- Render `/etc/hosts` from template so localhost entries and the host’s primary IPv4 mapping include the FQDN.

Variables:

- `domain_name`: DNS suffix appended to `inventory_hostname` for the FQDN (default in role defaults).

Notes:

- The playbook should use `gather_facts: true` so the `hosts` template can use default IPv4 facts.

### `rhel_dns_search_domain`

Responsibilities:

- Ensure an `append domain-search` line exists in the DHCP client configuration used for DNS search domains.
- Notify NetworkManager restart when that file changes.

Variables:

- `dns_search_domains`: comma-separated list of domains passed to `append domain-search` (default in role defaults).

Other:

- `dhclient_config_path`: path to the DHCP client config file (default `/etc/dhcp/dhclient.conf`, defined in `vars/main.yml`).

### `rhel_rhsm`

Responsibilities:

- Remove default cloud RHSM repo file.
- Install org CA certificate and update trust.
- Register system to Satellite/Capsule.

Variables:

- `sat_url`: Satellite URL
- `sat_username`: Satellite registration username.
- `sat_password`: Satellite registration password.
- `activation_key`: activation key for client registration.
- `org_id`: Satellite organization of hostgroup/client.
- `sat_env`: Satellite environment (e.g., dev, prod, etc.).
- `hostgroup`: hostgroup in Satellite that client will belong to.
- `location`: location of the hostgroup.
- `capsule_hostname`: Capsule/LB hostname.
- `capsule_url`: RHSM content base URL (`rhsm_baseurl` in role defaults).

### `rhel_os_partition`

Responsibilities:

- Install partitioning tools (`cloud-utils-growpart`, `gdisk`).
- Grow OS disk partition.
- Apply LVM/storage layout via `redhat.rhel_system_roles.storage`.
- Add `/tmp` to `/var/tmp` bind entry in `/etc/fstab`.

Variables:

- `fs_type`: filesystem type for created volumes (`xfs` by default).
- `volumes`: list of LVs (`name`, `size`, `fs_type`, `mount_point`).
- Size variables used by `volumes` defaults:

  - `rootlv_size`
  - `homelv_size`
  - `optlv_size`
  - `usrlv_size`
  - `tmplv_size`
  - `varlv_size`
  - `varloglv_size`
  - `auditloglv_size`

### `rhel_package_install`

Responsibilities:

- Install baseline packages, including minimal environment, AD/realm integration tools, and DNF plugin.

Variables:

- None in role defaults.

### `rhel_basic_config`

Responsibilities:

- Set locale to `en_US.UTF-8`.
- Configure keyboard settings file.
- Set timezone.
- Disable bluetooth service.
- Enable kernel audit flag (`audit=1`).

Variables:

- `timezone`: system timezone (default: `Pacific/Auckland`).

### `rhel_ntp`

Responsibilities:

- Configure chrony/NTP through `redhat.rhel_system_roles.timesync`.
- Set chrony custom settings and IPv4 NTP configuration.

Variables:

- `ntp_servers`: list of NTP servers consumed by timesync role.
- Optional helper variables used to build defaults:

  - `ntp_server1` (fallback: `nz.pool.ntp.org`)
  - `ntp_server2` (fallback: `0.rhel.pool.ntp.org`)

### `rhel_logrotation`

Responsibilities:

- Deploy `/etc/logrotate.conf`.
- Deploy rsyslog drop-in under `/etc/rsyslog.d/`.
- Restore SELinux labels under `/var/log`.

Variables:

- None in role defaults.

### `rhel_ssh`

Responsibilities:

- Add root authorized keys from role file.
- Set root password hash.
- Deploy hardened `sshd_config`, banner, and MOTD.
- Apply PAM custom files and symlinks when `authselect` is not installed.

Variables:

- `root_password`: encrypted root password hash.

### `rhel_swap`

Responsibilities:

- Deploy Azure swap cloud-init config from template.
- Set `CLOUD_CFG` environment in `/etc/systemd/system.conf`.

Variables:

- `file_ratio`: cloud-init disk file-system ratio (default: `66`).
- `swap_ratio`: cloud-init swap ratio (default: `33`).
- `cloud_cfg_file`: target cloud-init config path (defined in `vars/main.yml`, default `/etc/cloud/cloud.cfg.d/00-azure-swap.cfg`).

### `rhel_cleanup`

Responsibilities:

- Remove old kernels and clean DNF cache.
- Remove selected log/history/cache files.
- Remove `/tmp/*` and `/var/cache/dnf/*`.

Variables:

- `logfiles`: list of files/directories removed during cleanup.

## How to run

### Run full image build playbook

```bash
ansible-navigator run playbook_rhel_image_build.yml -i <inventory_file>
```

Example:

```bash
ansible-navigator run playbook_rhel_image_build.yml -i inventories/prod/hosts.yml
```

### Override variables at runtime

```bash
ansible-navigator run playbook_rhel_image_build.yml -i <inventory_file> \
  -e sat_username=<user> \
  -e sat_password=<password> \
  -e activation_key=<activation_key> \
  -e org_id=<org_id>
```

### Run a single role test playbook

```bash
ansible-navigator run roles/<role_name>/tests/test.yml -i roles/<role_name>/tests/inventory
```

Example:

```bash
ansible-navigator run roles/rhel_cleanup/tests/test.yml -i roles/rhel_cleanup/tests/inventory
```

## Notes

- `rhel_cleanup` is intended for image finalization. Review deletion scope before using on persistent systems.
- For RHEL 9, prefer managing PAM with `authselect` profiles where possible.
