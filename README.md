Sample playbook for installing open nebula

Needed to be able to quickly produce and repeat an install of open nebula.

## Requirements

For testing

* Vagrant 1.2.x
* Virtualbox 4.2.12

For production

* ubuntu 12.04

## The setup

The site.yml configures a single frontend machine and as many compute
nodes as necessary. Please define these in the hosts file, to deploy
a new opennebula installation (short of adding in the compute nodes to
oned) run the site.yml playbook. The compute node configuration assumes
kvm will be used.

The bridge configuration assumes that eth0 is to be used for br0 (it takes
the default networking information from ansible), this configuration is
stored in "playbooks/setup-bridge.yml"
