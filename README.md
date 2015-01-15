# debian-dnsmasq-pounder

This project stands up dnsmasq inside docker inside virtualbox via vagrant,
forwarding the following ports:

* localhost:60053/udp is forwarded to dnsmasq
* localhost:62375/tcp is forwarded to docker in the VM

## Dependencies

1. [vagrant](http://vagrantup.com]
1. [virtualbox](http://virtualbox.com]
1. [docker](http://docker.com]

## Configuration

* dnsmasq is configured by ```debian-dnsmasq-pounder/dnsmasq-conf/dnsmasq.conf```
* dnsmasq is configured (by default) to serve only the records included in ```debian-dnsmasq-pounder/dnsmasq-conf/hosts```

## Usage

1. clone this repo
1. ```cd``` into the repo dir
1. ```vagrant up```
 1. This will take some time, more/less depending on your bandwidth and system. It takes about 90 seconds on my system.
1. When it's finished, ```dig @localhost -p60053 one```.
1. ```echo '1.2.3.4 another.record' >> debian-dnsmasq-pounder/dnsmasq-conf/hosts```
1. ```docker -H tcp://localhost:62375 kill -s HUP $(docker -H tcp://localhost:62375 ps -q)```
1. ```dig @localhost -p60053 another.record```



