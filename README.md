Role Name
=========

Bare Deluged Role

Requirements
------------

It is only runable on Debian based machine. Tested with Ubuntu Bonic.

Caveat
------

- This role is designed to work on a dedicated seedbox.
- Modifing configurations directly, via `deluge-console` or WebUI will break the idempotence of the role.
- Some aspects of Deluge configuration are not supported. See [Role Variables](#role-variables) for more details.

Role Variables
--------------

Most of Deluge configuration are exposed via role variables. They are packed into group with mostly aligned name convention. They are tuned to match typical public seedbox requirement. Please lookat [`defaults/main.yml`](defaults/main.yml) to get all avalible variables.

##### Configuration NOT exposed:
  - Encryption
  - Proxy
  - Plugin
  - Auto Manage
  - GeoIP DB Location
  - Copy torrent in watch folder to another
  - Delete torrent file when remove
  - Allocation
  - Check new release
  - Logging
  - `info_sent` # Please tell me what it does and its parameter.
  - `send_info` # Please tell me what it does and its parameter.

Dependencies
------------

None.

Example Playbook
----------------

```yml
- hosts: servers
  become: yes
  become_user: root
  roles:
    - role: deluge
      vars:
        users:
          - name: su
            pass: ultrasecure
            level: 10
        config:
          daemon:
            port: 56607
          cache:
            size: 65536
```

Execute Playbook
----------------

You must have `ANSIBLE_HASH_BEHAVIOUR=merge` set before execute the playbook.

```shell
~$ ANSIBLE_HASH_BEHAVIOUR=merge ansible-playbook deluge.yml
```

License
-------

GPLv3


