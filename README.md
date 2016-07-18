# blueprint-fabric8
Performance-aware devops blueprint environment based on RedHat's fabric8

## How to setup
1. Install Ubuntu 16.04 on a physical or virtual machine
2. [Install the latest version of ansible](http://docs.ansible.com/ansible/intro_installation.html#latest-releases-via-apt-ubuntu)
3. Run `ansible-galaxy install angstwad.docker_ubuntu`
4. Configure the IP address of the machine in line 7 of `fabric8.yml`.
5. Run `ansible-playbook -c local fabric8.yml`
6. Fabric8 is then accessible at `http://fabric8.<ip-address-from-step-4>.xip.io`
