# vagrant-warzone2100
A vagrant VM provisioned with ansible 2 to build everything you need to compile and package as a deb warzone2100 master branch.

This VM will give you a stable environment to compile the current master branch of warzone2100 as well as all the libraries required to build .deb packages afterwards.

## Usage

Ensure ansible 2.0.0.x is installed

```
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible
```

from the cloned directory enter :

```
$ vagrant up
```

Leave it to build and when it's done :

```
$ vagrant ssh
```

To build warzone2100 from source

```
$ cd /vagrant/warzone2100
$ ./autogen.sh && ./configure && make
```

## Using ansible to provision your host Linux machine (ubuntu only at the moment but I will work on RHEL over the next couple of days)

edit the /etc/ansible/hosts and enter at the bottom :

```
[localhost]
127.0.0.1       ansible-connection=local
```
Edit .ansible/main.yml and change

```
hosts:all
```
to
```
hosts:localhost
```

Edit .ansible/roles/agent/defaults/main.yml and edit the clone_destination value to the folder you want to clone warzone to

Play the book with

```
$ ansible-playbook .ansible/main.yml
```
