## network-interfaces

[![Build Status](https://travis-ci.org/Oefenweb/ansible-network-interfaces.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-network-interfaces) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-network--interfaces-blue.svg)](https://galaxy.ansible.com/tersmitten/network-interfaces)

Manage network interfaces in Debian-like systems.

#### Requirements

None

#### Variables

##### General

* `network_interfaces_manage_devices`: [required]: Whether all additional scripts should be deleted
* `network_interfaces_interfaces`: [default: `[]`]: Network interfaces declarations
* `network_interfaces_interfaces.{n}.device`: [required]: Device name
* `network_interfaces_interfaces.{n}.triggers`: [default: `['auto']`]: When to enable|disable the interface
* `network_interfaces_interfaces.{n}.family`: [default: `inet`]: Network type, eg. inet | inet6
* `network_interfaces_interfaces.{n}.method`: [default: `dhcp`]: Method of the interface, eg. dhcp | static
* `network_interfaces_interfaces.{n}.<arbitrary_option>`: [default: ``]: Additional arbitrary option to the interface

##### Bridge

* `network_interfaces_interfaces.{n}.bridge`: [optional, default: `{}`]: Bridge declarations
* `network_interfaces_interfaces.{n}.bridge.ports`: [optional]: Bridge ports
* `network_interfaces_interfaces.{n}.bridge.stp`: [optional]: Turn spanning tree protocol on/off
* `network_interfaces_interfaces.{n}.bridge.fd`: [optional]: Bridge forward delay
* `network_interfaces_interfaces.{n}.bridge.maxwait`: [optional]: Maximum time to wait for the bridge ports to get to the forwarding status
* `network_interfaces_interfaces.{n}.bridge.waitport`: [optional]: Maximum time to wait for the specified ports to become available 

##### Inline hook scripts

* `network_interfaces_interfaces.{n}.pre-up`: [optional, default: `[]`]: List of pre-up script lines
* `network_interfaces_interfaces.{n}.up`: [optional, default: `[]`]: List of up script lines
* `network_interfaces_interfaces.{n}.down`: [optional, default: `[]`]: List of down script lines
* `network_interfaces_interfaces.{n}.post-down`: [optional, default: `[]`]: List of post-down script lines


## Dependencies

None

#### Example(s)

##### DigitalOcean droplet with private networking enabled

```yaml
---
- hosts: all
  roles:
    - network-interfaces
  vars:
    network_interfaces_manage_devices: true
    network_interfaces_interfaces:
      - device: eth0
        triggers: ['auto']
        family: inet
        method: static
        address: 188.166.9.28
        netmask: 255.255.0.0
        gateway: 188.166.0.1
        mtu: 1500
        dns-nameservers: "8.8.8.8 8.8.4.4"
        up:
          - 'ip addr add 10.18.0.8/16 dev eth0'
      - device: eth1
        triggers: ['auto']
        family: inet
        method: static
        address: 10.133.136.172
        netmask: 255.255.0.0
```

#### License

MIT

#### Author Information

* Andreas Reischuck
* Mark van Driel
* Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-network-interfaces/issues)!
