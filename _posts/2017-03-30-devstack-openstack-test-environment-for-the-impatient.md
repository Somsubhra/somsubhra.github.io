---
layout: post
title: DevStack - OpenStack test environment for the impatient
---

If you are working with [OpenStack](http://openstack.org) and you do not want a full fledged installation of OpenStack for testing, you can check out [DevStack](http://devstack.org). It is a set of scripts which will setup a test OpenStack environment in a few minutes with one simple script on a single node.

In my case, I used a 12G Virtual Machine with 6 CPU cores, 200G disk and Ubuntu 16.04 as the Linux OS. 

- The first step is to add a user with sudo priveleges. I created a user called `stack` here, added it to the sudoers list and switched to that user shell.

```
$ sudo useradd -s /bin/bash -d /opt/stack -m stack
$ sudo tee <<<"stack ALL=(ALL) NOPASSWD: ALL" /etc/sudoers
$ sudo su - stack
```

- Next download devstack from the git repository.

```
$ git clone https://git.openstack.org/openstack-dev/devstack
$ cd devstack
```

- You now need to add configuration for OpenStack admin password, database password, etc. In the root of the `devstack` directory create a `local.conf` file and add the following.

```
[[local|localrc]]
ADMIN_PASSWORD=admin
DATABASE_PASSWORD=$ADMIN_PASSWORD
RABBIT_PASSWORD=$ADMIN_PASSWORD
SERVICE_PASSWORD=$ADMIN_PASSWORD
```

- Now you are all set to start the installation. Just run

```
$ ./stack.sh
```

You will see a bunch of packages downloading and getting installed. Wait for the process to exit successfully - and yes, you are done with your OpenStack test installation.

You can open the OpenStack Horizon Dashboard at [http://devstack_box_url/](http://devstack_box_url/).
