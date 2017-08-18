Matterircd
==========

A role that installs and can configure [matterircd](https://github.com/42wim/matterircd).

This role installs a versioned binary of matterircd in `/opt/matterircd`, adds a systemd unit file and (re)starts matterircd.

Requirements
------------

An ansible 2.0+ installation.

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

    matterircd_version: 0.14.0
    mattermost_tar_checksum: 'sha256:48270C1264E8E689A961382E2A148FAFBFDAF986223FE7A3EB308D07CCCE6BAB'

The version of matterircd to install and the file's checksum.
This role installs matterircd to `/opt/matterircd/matterircd-{{ matterircd_version }}` and sets the unit-file to use that binary in `ExecStart`.
This allows for upgrades and downgrades.

    matterircd_bind: '127.0.0.1:6667'

The address and port matterircd listens on.

    matterircd_user: matterircd

The user to run matterircd as, will be created if it does not exist.

    matterircd_mmserver: ''

Specify to set the default mattermost server/instance. This passes the [`-mmserver`](https://github.com/42wim/matterircd#usage) option to the binary.

    matterircd_mmteam: ''

Specify default mattermost team. This passes the [`-mmteam`](https://github.com/42wim/matterircd#usage) option to the binary.

    matterircd_restrict: "{{ matterircd_mmserver }}"

Only allow connection to specified mattermost server/instances. This passes the [`-mmrestrict`](https://github.com/42wim/matterircd#usage) option to the binary.

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
     - { role: pieterlexis.matterircd,
         matterircd_mmserver: 'mattermost.corp.example',
         matterircd_mmteam: 'myteam' }
```

License
-------

MIT

Author Information
------------------

 * Pieter Lexis
