Icinga2
=========

Simple role for setup and configuration of Icinga2. For now only client and satellites are supported.

Requirements
------------

none

Role Variables
--------------

```
icinga2_rebuild_certificates: no
icinga2_accept_commands: yes
icinga2_accept_config: yes
icinga2_disable_confd: yes
icinga2_global_zones: []
icinga2_pki_path: /var/lib/icinga2/certs
icinga2_setup: yes
icinga2_cn: "{{ inventory_hostname }}"
icinga2_zone: "{{ inventory_hostname }}"
# communication: master -> client
icinga2_endpoint: "{{ icinga2_master }}"
# communication: client -> master
icinga2_endpoint:
  name: "{{ icinga2_master }}"
  host: "{{ icinga2_master }}"
  port: 5665
icinga2_parent_host: "{{ icinga2_master }}"
icinga2_parent_zone: "master"
```

Dependencies
------------

None

Example Playbook
----------------

Simple example with one master and some additional check plugins

    - hosts: servers
      vars:
        # icinga2 master, which is also the endpoint
        icinga2_master: "icinga-master.example.org"

        # list of additional check plugins
        icinga2_plugins:
          - check_unicorn
      roles:
        - { role: nbuchwitz.icinga2 }


License
-------

GNU General Public License v2.0

Author Information
------------------

Nicolai Buchwitz <nb@tipi-net.de>
