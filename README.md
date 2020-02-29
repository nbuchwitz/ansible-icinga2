Icinga2
=========

Installs and configures Icinga2 on RHEL/CentOS or Debian/Ubuntu servers.

Requirements
------------

This role needs root access for setup and configuration. Use either a global ``become: True`` or use it in your role definition like this:

```
- hosts: client
  role:
    - role: nbuchwitz.icinga2
      become: True
```

Role Variables
--------------

```
icinga2_master: master.example.org
```

Icinga2 master for ticket generation.

```
icinga2_setup: yes
```

Install Icinga repositories and packages.

```
icinga2_cn: "{{ inventory_hostname }}"
```

The name of the Icinga host.

```
icinga2_zone: "{{ inventory_hostname }}"
```

The zone of the Icinga host.

```
icinga2_endpoint: "{{ icinga2_master }}"
```

Connect to remote endpoint (parent communicates with child). See [Icinga distributed monitoring documentation](https://icinga.com/docs/icinga2/latest/doc/06-distributed-monitoring/) for more details.

```
icinga2_endpoint:
  name: "{{ icinga2_master }}"
  host: "{{ icinga2_master }}"
  port: 5665
```

Connect to remote endpoint (child communicates with parent, useful in NAT environments). See [Icinga distributed monitoring documentation](https://icinga.com/docs/icinga2/latest/doc/06-distributed-monitoring/) for more details.


```
icinga2_parent_host: "{{ icinga2_master }}"
```

The name of the parent host for auto-signing the CSR.

```
icinga2_parent_zone: "master"
```

The name of the parent zone.

```
icinga2_user: icinga
icinga2_group: icinga
```

User and group of the Icinga daemon. Used in permissions.

```
icinga2_rebuild_certificates: no
```

If set to yes/true existing certificates will be removed and new ones will be created.

```
icinga2_global_zones: []
```

List of additional global zones. See [Icinga documentation](https://icinga.com/docs/icinga2/latest/) for more details.

```
icinga2_accept_commands: yes
icinga2_accept_config: yes
```

Accept config and commands from parent / master. See [Icinga documentation](https://icinga.com/docs/icinga2/latest/) for more details.

```
icinga2_disable_confd: yes
```

Disable the default configuration directory. Should be touched unless this is a standalone instance.

```
icinga2_pki_path: /var/lib/icinga2/certs
```

Override default Icinga pki path. This shouldn't be necessary for most environments.


Dependencies
------------

None

Example Playbook
----------------

Simple example with one master and some additional check plugins

```
- hosts: servers
  become: True
  vars:
    # icinga2 master, which is also the default endpoint
    icinga2_master: "master.example.org"

    # list of additional check plugins
    icinga2_plugins:
      - check_unicorn
  roles:
    - nbuchwitz.icinga2
```


License
-------

GNU General Public License v2.0

Author Information
------------------

Nicolai Buchwitz <nb@tipi-net.de>
