[![Build Status](https://travis-ci.org/wtanaka/ansible-role-zookeeper.svg?branch=master)](https://travis-ci.org/wtanaka/ansible-role-zookeeper)
[![CircleCI](https://circleci.com/gh/wtanaka/ansible-role-zookeeper.svg?style=svg)](https://circleci.com/gh/wtanaka/ansible-role-zookeeper)

wtanaka.zookeeper
=================

Installs Apache ZooKeeper

Requires that you have java installed already, e.g. using
https://galaxy.ansible.com/wtanaka/oracle-java/

Example Playbook
----------------

    - hosts: servers
      roles:
         - role: wtanaka.zookeeper
           # My own server ID
           zookeeper_myid: 1
           zookeeper_config:
             # The number of milliseconds of each tick
             tickTime: 2000
             # the directory where the snapshot is stored.
             dataDir: /var/lib/zookeeper
             clientPort: 2181
             # The number of ticks that the initial
             # synchronization phase can take
             initLimit: 10
             # The number of ticks that can pass between
             # sending a request and getting an acknowledgement
             syncLimit: 5
           # This variable is treated the same way as zookeeper_config
           # currently, but is separated out so that it can be varied
           # based on inventory while zookeeper_config can be set in
           # group_vars
           zookeeper_server_config:
             # specify all zookeeper servers
             # The fist port is used by followers to connect to the leader
             # The second one is used for leader election
             "server.1": zookeeper1:2888:3888
             "server.2": zookeeper2:2888:3888
             "server.3": zookeeper3:2888:3888

### Other variables

#### `zookeeper_should_shortcircuit`

Default: True

When True, this role short-circuits itself if a "xxxx" is already in
the path

#### `zookeeper_state`

Legal values: `started`, `stopped`, `restarted`, `reloaded`

This is passed into the service task that determines the initial state of the service

#### `zookeeper_enabled`

Legal values: `yes`, `no`

This is passed into the service task that determines whether zookeeper is enabled at computer startup

License
-------

GPLv2

Author Information
------------------

http://wtanaka.com/
