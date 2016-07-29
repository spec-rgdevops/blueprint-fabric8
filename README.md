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

![](graphics/fabric8-diagram.png)

## fabric8 user

To use fabric8 you can now log into the master node via SSH and setup a user:
	
	$ sudo htpasswd /etc/origin/master/htpasswd <username>

To add cluster-admin rights to this user:

	$ oadm policy add-cluster-role-to-user cluster-admin <username>

## use fabric8

Now you can use fabric8 by simply accessing http://fabric8.oc.master.example.org (or whatever your domain is). Login with the user just created.

## Troubleshooting

**Ansible reports UNREACHABLE**

In our testing environment sometimes during playing the playbook there has been an error reporting an SSH-error resulting in an abort with the failure UNREACHABLE. There seems to be no specific reason (probably just SSH temporarily unavailable) and you can just rerun the playbook from the beginning.

**fabric8 is not available**

Ensure the router and registry pods are running:

	$ oc get pods

If they are not running (pending) you can check the reasons for that by entering:

	$ oc describe pod <podname>

If your master node is not marked as schedulable, this could be a reason. Schedulable means that a pod can be deployed on this node. In this case run:

	$ oadm manage-node master.example.com --schedulable=false

##Further information

These are some helpful links where you can get help, if you are in trouble with the installation:

- Openshift advanced Installation: [https://docs.openshift.org/latest/install_config/install/advanced_install.html](https://docs.openshift.org/latest/install_config/install/advanced_install.html "https://docs.openshift.org/latest/install_config/install/advanced_install.html")
- Openshift-Ansible on GitHub: [https://github.com/openshift/openshift-ansible](https://github.com/openshift/openshift-ansible "https://github.com/openshift/openshift-ansible")
- GetStarted fabric8 on OpenShift: [https://fabric8.io/guide/getStarted/openshift.html](https://fabric8.io/guide/getStarted/openshift.html "https://fabric8.io/guide/getStarted/openshift.html")
