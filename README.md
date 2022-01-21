# Ansible Vagrant profile for hacking the ansible datapower collection

## Getting Started

  1. Download and Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
  2. Download and Install [Vagrant](https://www.vagrantup.com/downloads.html)
  3. Install [Ansible](http://docs.ansible.com/ansible/latest/intro_installation.html)
  4. Open a shell prompt and cd into the folder containing the `Vagrantfile`
  5. Run the following command to install the necessary Ansible roles for this profile: `$ ansible-galaxy install -r requirements.yml`

Once all of that is done, you can simply type in `vagrant up`, and Vagrant will create a new VM, install the base box, and configure it.

Once the new VM is up and running (after `vagrant up` is complete and you're back at the command prompt), you can log into it via SSH if you'd like by typing in `vagrant ssh`.

## Hacking

Log into vagrant VM with `vagrant ssh` and become root with `sudo -i`.  Change your working directory to `/root/ansible_collections/br35ba56/datapower`.  Test commands must be ran within this directory.

Run sanity tests with `ansible-test sanity --docker`
Run unit tests with `ansible-test units --docker`


Integration testing requires a datapower docker container to be running prior to executing integration tests.  Start it and update the inventory with the following commands:
```
docker run -d --name datapower tonyschndr/datapower:10.0.1.4
HOST_IP=$(docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' datapower)
sed -i "s/{{HOST_IP}}/$HOST_IP/g" /root/ansible_collections/br35ba56/datapower/tests/integration/inventory.networking
```

Now that the container is started run `ansible-test network-integration --docker`