[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)
[![ReadTheDocs](https://readthedocs.org/projects/microfirewall/badge/?version=latest)](https://microfirewall.readthedocs.io/)

Building OpenWRT with the MFW Feed
=======================================

The steps below describe building an OpenWRT x86 image with support for
running packetd. This is accomplished by pulling in a custom feed with
the packetd application and a couple of dependencies.

The Docker build method uses a volume to perform the build, you can mix
both methods at any time: the build results will always be on your local
disk.

Building in Docker:
-------------------

Grab the MFW-patched OpenWRT git repository:
```
git clone https://github.com/untangle/openwrt.git
cd openwrt
```

Build it for your intended device and libc targets:
```
docker-compose -f mfw/docker-compose.build.yml run build (-d x86_64|wrt1900|wrt3200|omnia, -l musl|glibc)
```

The OpenWRT documentation warns that building with -jN can cause
issues. If you hit a failure with -jN the first thing to do is to rerun
with -j1. Adding V=s increases verbosity so that you'll have output to
look at when/if something still fails to build:

```
docker-compose -f mfw/docker-compose.build.yml run build (-d x86_64|wrt1900|wrt3200|omnia, -l musl|glibc) -m "-j1 V=s"
```

Building directly on a Stretch host:
------------------------------------

Install build dependencies:
```
apt-get install build-essential curl file gawk gettext git libncurses5-dev libssl-dev python2.7 swig time unzip wget zlib1g-dev
```

Grab the MFW-patched OpenWRT git repository:
```
git clone https://github.com/untangle/openwrt.git
cd openwrt
```

Build it for your intended libc target:
```
./mfw/build.sh [-d (x86_64|wrt1900|wrt3200|omnia)] [-l (musl|glibc)] [-v (<branch>|<tag>|release)]
```

The OpenWRT documentation warns that building with -jN can cause
issues. If you hit a failure with -jN the first thing to do is to rerun
with -j1. Adding V=s increases verbosity so that you'll have output to
look at when/if something still fails to build:
```
./mfw/build.sh [-d (x86_64|wrt1900|wrt3200|omnia)] [-l (musl|glibc)] [-v (<branch>|<tag>|release)] -m "-j1 V=s"
```

Setting up a VM
===============

If everything built correctly you should have a gzipped image in the
bin directory (to use with for instance QEMU):
```
gunzip bin/targets/x86/64*/openwrt-x86-64-combined-ext4.img.gz
```

There is also a VirtualBox disk image:
```
bin/targets/x86/64*/openwrt-x86-64-combined-ext4.vdi
```

Read further instructions below for VirtualBox

In QEMU
-------
To launch OpenWRT x86\_64 in QEMU, make sure br0 is a pre-existing
bridge with external access. On my machine, it looks like this, with
eth0 being the actual physical interface connected to my network:
```
# ip ad show br0
3: br0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether e0:cb:4e:a9:80:64 brd ff:ff:ff:ff:ff:ff
    inet 172.17.17.6/24 brd 172.17.17.255 scope global br0
       valid_lft forever preferred_lft forever
# ip ad show eth0
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state UP group default qlen 1000
    link/ether e0:cb:4e:a9:80:64 brd ff:ff:ff:ff:ff:ff
```

Then run something like (br10 will be created dynamically):
```
~/ngfw_pkgs/untangle-development-kernel/files/usr/bin/ut-qemu-run -f openwrt-x86-64-combined-ext4.img -b br0 -c br10 -t g
```

In Virtualbox
-------------

Create a new VM using the vdi image, but *do not boot it* before
changing its network settings: you want the 1st interface to be some
some of an internal net, without a need for connectivity (this will be
eth0, which OpenWRT uses as its internal interface), and the 2nd
interface should ideally be bridged (this will be eth1, used as the
external interface by OpenWRT)

Beware: SSH will by default not require a password!

Running the image
=================

Accessing the host
------------------

You can now ssh into your the host's eth1 IP, which it should have
grabbed from DHCP through your bridged interface:
```
ip ad show eth1
```

Using the OpenWRT admin UI
--------------------------

You can also install the OpenWRT admin UI if you need it:
```
opkg update
opkg install uhttpd
opkg install luci
```

Installing extra programs
-------------------------

Other useful programs can also be added, for instance:
```
opkg install tcpdump
```

Trying out packetd
==================

packetd is started by default by procd and listens on port 8080 for now.

You can stop it with:

```
/etc/init.d/packetd stop
```

To run it in the foreground where you can see debugging output just run:
```
packetd
```

Developer info: maintaining untangleinc/mfw:x86-64 in DockerHub
===============================================================

Using a build from 2019-03-20 as an example:

```
cd build
docker build -f Dockerfile.test.mfw --build-arg ROOTFS_TARBALL=sdwan-x86-64-generic-rootfs_v0.1.0beta1-44-g1003464fea_20190321T0728.tar.gz -t untangleinc/mfw:x86-64_20190320 .
docker tag untangleinc/mfw:x86-64_20190320 untangleinc/mfw:x86-64 
docker push untangleinc/mfw:x86-64 
```
