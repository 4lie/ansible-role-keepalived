# Ansible Role Keepalived

Ansible Role for setting up keepalived.

This Role sets up Keepalived for an standard setup of:

  - One virtual IP
  - Two hosts

You just need to provide an small amount of information to have it running

  - Add "keepalived" role to both hosts
  - Add variable keepalived_role: "MASTER" | "BACKUP" to the appropiate hosts 
  - Add variable keepalived_shared_ip: "floating IP address" to both hosts

Other variables can be configured, overwriting defaults/main.yml

Keepalived can watch processes to influence on which node should be the master.
Setting variable "keepalived_check_process" to the name of the process will do. 
I use Keepalived to give high availability to HAProxy, so I use.

keepalived_check_process: "haproxy"

Dependencies
------------

Works with centos/redhat and Debian/Ubuntu

Installation
-------------------------

```
# requirments.yaml
- src: git@github.com:4lie/ansible-role-keepalived.git
  scm: git
  version: master
  name: keepalived
```

Role Variables
--------------

```
keepalived_auth_pass: "secret"
keepalived_role: "MASTER"
keepalived_router_id: "52"
keepalived_shared_iface: "eth0"
keepalived_shared_ip: "192.168.1.1"
keepalived_check_process: "keepalived"
keepalived_priority: "100"
keepalived_backup_priority: "50"
```

Example Playbook
-------------------------

```
- hosts: s1
  roles:
      - { role: keepalived, keepalived_shared_ip: "192.168.1.1", keepalived_role: "MASTER" }

- hosts: s2
  roles:
      - { role: keepalived, keepalived_shared_ip: "192.168.1.1", keepalived_role: "BACKUP" }
```
