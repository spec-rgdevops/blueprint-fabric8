# blueprint-fabric8
Performance-aware devops blueprint environment based on RedHat's fabric8

## How to setup
These steps are to be executed on the target machine.

1. Install Ubuntu 16.04 on a physical or virtual machine
2. [Install the latest version of ansible](http://docs.ansible.com/ansible/intro_installation.html#latest-releases-via-apt-ubuntu)
3. Run `ansible-galaxy install angstwad.docker_ubuntu`
4. Clone this repository or download `fabric8.yml` to an arbitrary directory.
5. Configure the IP address in line 7 of `fabric8.yml`. This is the public IP address of the machine.
6. Run `ansible-playbook -c local fabric8.yml`
7. Fabric8 is then accessible at `http://fabric8.<ip-address-from-step-5>.xip.io`
