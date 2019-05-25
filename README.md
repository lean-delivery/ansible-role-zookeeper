Zookeeper installation
=========
[![License](https://img.shields.io/badge/license-Apache-green.svg?style=flat)](https://raw.githubusercontent.com/lean-delivery/ansible-role-zookeeper/master/LICENSE)
[![Build Status](https://travis-ci.org/lean-delivery/ansible-role-zookeeper.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-zookeeper)
[![Build Status](https://gitlab.com/lean-delivery/ansible-role-zookeeper/badges/master/build.svg)](https://gitlab.com/lean-delivery/ansible-role-zookeeper/pipelines)
[![Galaxy](https://img.shields.io/badge/galaxy-lean__delivery.zookeeper-blue.svg)](https://galaxy.ansible.com/lean_delivery/zookeeper)
![Ansible](https://img.shields.io/ansible/role/d/36578.svg)
![Ansible](https://img.shields.io/badge/dynamic/json.svg?label=min_ansible_version&url=https%3A%2F%2Fgalaxy.ansible.com%2Fapi%2Fv1%2Froles%2F36578%2F&query=$.min_ansible_version)

This role:
  - Installs ZooKeeper
  - Configures it as a single node or a cluster

Requirements
------------

 - Minimal Version of the ansible for installation: 2.7
 Supported OS:
   - CentOS
       7
   - Ubuntu
    - 16.04
    - 18.04
  - Debian
    - 9

Role Variables
--------------

 - `zk_version` -  version of the package

    default: `3.4.14`

 - `zk_url` - download url

    default: `http://www.us.apache.org/dist/zookeeper/zookeeper-{{zk_version}}/zookeeper-{{zk_version}}.tar.gz` for versions < 3.5

    default: `http://www.us.apache.org/dist/zookeeper/zookeeper-{{zk_version}}/apache-zookeeper-{{zk_version}}-bin.tar.gz` for versions 3.5.x

 - `zk_tarball_installation` - installation from tarball(or repository)

    default: `true`

 - `zk_user` - OS user name for zookeeper

    default: `zookeeper`

 - `zk_group` - OS user group name for zookeeper

    default: `zookeeper`

 - `zk_debian_apt_repositories` -  path to apt repository

    default: `"deb http://us-east1.gce.archive.ubuntu.com/ubuntu/ bionic universe"`

 - `zk_redhat_yum_repositories` -  path to yum repository

    default: `- https://archive.cloudera.com/cdh5/one-click-install/redhat/7/x86_64/cloudera-cdh-5-0.x86_64.rpm`

 - `zk_client_port` - zookeeper port

    default: `2181`

 - `zk_init_limit` - amount of time in ticks to allow followers to connect and sync to a leader

    default: `5`

 - `zk_sync_limit` - amount of time in ticks to allow followers to sync with ZooKeeper

    default: `2`

 - `zk_tick_time` - it is used to regulate heartbeats, and timeouts. For example, the minimum session timeout will be two ticks

    default: `2000`

 - `zk_autopurge_purgeInterval` - the time interval in hours for which the purge task has to be triggered

    default: `0`

 - `zk_autopurge_snapRetainCount` - when enabled, ZooKeeper auto purge feature retains the autopurge.snapRetainCount most recent snapshots and the corresponding transaction logs in the dataDir and dataLogDir respectively and deletes the rest

    default: `10`

 - `zk_data_dir` - libraries directory

    default: `/var/lib/zookeeper`

 - `zk_log_dir` - logs directory

    default: `/var/log/zookeeper`

 - `zk_dir` - zookeeper direcotry

    default: `"{{ zk_tarball_installation | ternary('/opt/zookeeper-' + zk_version, '/usr/lib/zookeeper') }}"`

 - `zk_force_myid` - to reset id

    default: `true`

 - `zk_force_config` - to rewrite config files

    default: `true`

 - `zk_tarball_dir` - place where you download tarball

    default: `/opt/src`

 - `zk_rolling_log_file_max_size` - zookeeper log file size

    default: `10MB`

 - `zk_max_rolling_log_file_count`- zookeeper log file count

    default: `10`

 - `zk_inventory_group` - zookeeper inventory group name

    default: `zookeeper`

  - `zk_service_name` - zookeeper service name

    default: `zookeeper`

  - `zk_service_start` - to start zookeeper service in the end of role/Playbook

    default: `true`

  - `zk_service_autostart` - Add zookeeper service to automatically start.

    default: `true`

  - `zk_reconfig_enabled` - This option is introduced such that the reconfiguration feature can be completely disabled and any attempts to reconfigure a cluster through reconfig API with or without authentication will fail by default

    default: `true`

Dependencies
------------

https://github.com/lean-delivery/ansible-role-java

Example Inventory
----------------
```ini
 [zookeeper]
 zookeeper1 zk_server_role=participant
 zookeeper2 zk_server_role=observer
 zookeeper3
 ```

  - `zk_server_role` - zookeeper server role. Host variable. Variables: participant, observer

    default:  participant

Example Playbook
----------------

```yaml
- name: Installing ZooKeeper
  hosts: zookeeper
  roles:
    - role: lean_delivery.java
    - role: lean_delivery.zookeeper
      zk_inventory_group: zookeeper
```


License
-------
Apache

Author Information
------------------

authors:
  - Lean Delivery Team <team@lean-delivery.com>
