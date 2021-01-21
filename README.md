# Proftpd

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/proftpd/status.svg)](https://drone.osshelp.ru/ansible/proftpd)

Ansible role, which installs proftpd, set parameters for it and add proftpd virtual users if set any.

## Deploy example

```yaml
  roles:
    - { role: proftpd,
        proftpd_params: [
          { key: PassivePorts, value: '60000 61000' },
          { key: MasqueradeAddress, value: '1.2.3.4' }
        ],
        enable_virtual_users: yes,
        ftp_users: [
          { name: "proftpd_test",
            uid: 1000,
            gid: 1000,
            home: /tmp,
            shell: /bin/false,
            password: this_must_be_vaulted_in_real_playbook
          },
          { name: "proftpd_test2",
            uid: 1001,
            gid: 1001,
            home: /tmp,
            shell: /bin/false,
            password: this_must_be_vaulted_in_real_playbook
          }
        ]
    }
```

You can control most parameters from proftpd.conf. Use for this "params" array, like shown in example.
Key is parameter name from proftpd.conf and value is what would be placed after key and space.

## By default role uses these variables (default params in proftpd.conf, no virtual users)

```yaml
packages:
  - proftpd
  - apg

conf_path: /etc/proftpd/proftpd.conf
custom_conf_dir: /etc/proftpd/conf.d

place_user_creation_script: no
user_creation_script_dir: '/usr/local/etc/proftpd_user_creator'
enable_virtual_users: no
proftpd_params: []
ftp_users: []
```
