MYZ vagrant machine
===================

OS: CentOS 7
Provisioning: Ansible
Tested with Vagrant v 1.7.4

Requirements
------------------------
1.Virtualbox, Vagrant
2. Ansible installed (See http://docs.ansible.com/ansible/intro_installation.html)

3. Two dir have to be created to be mapped:

    $ mkdir ../myzanichelli_source_v2
    $ mkdir ../myzanichelli_source

4. Vagrant plugin hostmanager have to be installed

    $ vagrant plugin install vagrant-hostmanager


To start machine type
------------------------
    $ vagrant up --provision

Note:
acceptance_tests role have to be installed first
to not to have conflicts between desktop (@xfce)
packages and epel repo packages