# Deploying OpenNebula

Needed to be able to quickly produce and repeat an install of OpenNebula.

## Requirements

For testing

* Vagrant 1.2.x
* Virtualbox 4.2.12

For production

* Ubuntu 12.04

## The setup

The site.yml configures a single frontend machine and as many compute
nodes as necessary. Please define these in the hosts file, to deploy
a new opennebula installation (short of adding in the compute nodes to
oned) run the site.yml playbook. The compute node configuration assumes
kvm will be used.

The bridge configuration assumes that eth0 is to be used for br0 (it takes
the default networking information from ansible), this configuration is
stored in "playbooks/setup-bridge.yml"

## Typical setup process

* install machines with basic ubuntu server install (use preseed or kickstart to automate it)
* create a hosts file
* set the root passwords (if they are not secure) on the machines to be the same and upload your public ssh-key
  - ansible-playbook -i hosts playbook/setup-root-passwd.yml -k
  - ansible-playbook -i hosts playbook/setup-upload-public-key-to-root.yml -k
* run the playbooks to deploy the front-end and compute nodes
  - look at playbooks/setup-bridge.yml if you are interested in configuring a bridge
  - look at playbooks/setup-nfs-exports.yml if you just want to use nfs as the shared datastore
  - look at playbooks/setup-apparmor.yml to fix up apparmor issue
  - deploy ceph keys and configs to compute nodes if necessary
  - there are a number of other 'plays' which can aid in setting up an opennebula cluster
* once the base system is up, the admin can go to the sunstone interface at http://opennebula-frontend:9869/

## Typical testing/development setup process

    git clone https://github.com/jcftang/ansible-opennebula.git
    cd ansible-opennebula
    cd hacking
    vagrant up
    source env-setup
    cd ..
    ansible-playbook site-vagrant.yml

Once the playbook has finished, you should be able to access the VM from
your machine on this address -- http://192.168.206.110:9869/
