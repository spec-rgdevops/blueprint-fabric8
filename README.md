# blueprint-fabric8
Performance-aware devops blueprint environment based on RedHat's fabric8

## Deployment
We deployed our fabric8 blueprint environment based on Docker and OpenShift on Ubuntu.
In this repo there is a ansible playbook available to run to setup a local OpenShift cluster consisting of one all-in-one node.

To run the playbook you first need to install ansible (cf.  [http://docs.ansible.com/ansible/intro_installation.html#latest-releases-via-apt-ubuntu]):

```
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible
```

Also you need to install a role from ansible galaxy, which we reused to install Docker on Ubuntu:

```
$ ansible-galaxy install angstwad.docker_ubuntu
```

Finally adjust the variables of the playbook to your needs and run it:

```
$ sudo ansible-playbook fabric8-anspb.yml
```
