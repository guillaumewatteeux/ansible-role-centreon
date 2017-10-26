Centreon
==========

Ansible [Centreon](http://www.centreon.com) role.

Features:
 * Create / manage host on Centreon instance
 * Deploy service with hostTemplate
 * Deploy service from mountpoint

Require
--------

centreonapi
```
pip install https://github.com/guillaumewatteeux/centreon-sdk-python/releases/download/v0.0.2/centreonapi-0.0.2.tar.gz
```

Role Variables
--------------

see `defaults/main.yml`

Example Playbook
----------------

    - hosts: all
      roles:
        - role: guillaumewatteeux.centreon
          centreon_hostgroups:
            - name: "MyProject"
              alias: "My First Project"
            - name: "_dev"
              alias: "dev"
          centreon_host_hostgroups:
            - "MyProject"
            - "_dev"
          tags:
            - centreon

    - hosts: mysql_servers
      roles:
        - role: guillaumewatteeux.centreon
          centreon_host_hosttemplates: App-DB-MySQL-custom
          centreon_host_macros:
            - name: "MYSQLPASSWORD"
              value: "{{ vault_sql_users_passwords[ansible_fqdn]['centreon'] }}"
            - name: "MYSQLPORT"
              value: 3306
            - name: "MYSQLUSERNAME"
              value: "centreon"


Automaticly create hostgroups for "MyProject" and "dev". Create new host and link to hostgroup.

`monitoring_ip`: define alternative IP for host (example: VPN IP)

License
-------

Apache 2.0
