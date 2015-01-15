# debian-dnsmasq-pounder

## Dependencies

1. [vagrant](http://vagrantup.com]
1. [virtualbox](http://virtualbox.com]
1. [docker](http://docker.com]

## Usage

```vagrant up``` to start dnsmasq (in a Debian docker image) on localhost port
60053.

* dnsmasq is configured by
  ```debian-dnsmasq-pounder/dnsmasq-conf/dnsmasq.conf```
* dnsmasq is configured (by default) to serve only the records included in
  ```debian-dnsmasq-pounder/dnsmasq-conf/hosts```

### Example

1. clone this repo
1. ```cd``` into the repo dir
1. ```vagrant up```
1. When it's finished, ```dig @localhost -p60053 one```.
1. ```echo '1.2.3.4 another.record' >>
   debian-dnsmasq-pounder/dnsmasq-conf/hosts```
1. ```dig @localhost -p60053 another.record```



