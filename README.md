# blueprint-fabric8
Performance-aware devops blueprint environment based on RedHat's fabric8

This repository contains an ansible playbook and an example host-file to setup an OpenShift cluster (this is based on [https://github.com/openshift/openshift-ansible](https://github.com/openshift/openshift-ansible "https://github.com/openshift/openshift-ansible") and deploy fabric8 on top of that.

## Requirements
- Ansible >v2.1
- git
- Requirements for the hosts: [https://docs.openshift.org/latest/install_config/install/prerequisites.html#system-requirements](https://docs.openshift.org/latest/install_config/install/prerequisites.html#system-requirements "https://docs.openshift.org/latest/install_config/install/prerequisites.html#system-requirements")

## Configuring the Installation
To configure the installation have a look at the `oc.hosts` file.
To get further help, have a look at [https://docs.openshift.org/latest/install_config/install/advanced_install.html](https://docs.openshift.org/latest/install_config/install/advanced_install.html "https://docs.openshift.org/latest/install_config/install/advanced_install.html").

## Running the Ansible Playbook
To execute the playbook you first need to clone the openshift-ansible repo as a submodule:

	$ git submodule add git@github.com:openshift/openshift-ansible.git openshift-ansible

The playbook will setup Docker, an OpenShift-Cluster and will run the fabric8-Installer gofabric8 on the master.

    $ ansible-playbook oc-setup.yml -i oc.hosts

## fabric8 user
To use fabric8 you can now log into the master node via SSH and setup a user:
	
	$ htpasswd /etc/origin/master/htpasswd <username>

To add cluster-admin rights to this user:

	$ oadm policy add-cluster-role-to-user cluster-admin <username>