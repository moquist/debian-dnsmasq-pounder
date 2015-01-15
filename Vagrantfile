VAGRANTFILE_API_VERSION = "2"

Vagrant.require_version ">= 1.6.3"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "debian-dnsmasq-pounder"

  config.vm.box = "yungsang/boot2docker"

  config.vm.synced_folder ".", "/vagrant"

  config.vm.provision :docker do |d|
    d.build_image "/vagrant/debian-dnsmasq-pounder",
      args: "-t moquist/debian-dnsmasq-pounder"
    d.run "dnsmasq",
      image: "moquist/debian-dnsmasq-pounder",
      args: "-p 60053:60053/udp -v /vagrant/debian-dnsmasq-pounder/dnsmasq-conf:/opt/dnsmasq-conf:ro",
      cmd: "/usr/sbin/dnsmasq -C /opt/dnsmasq-conf/dnsmasq.conf -d"
  end

  config.vm.network :forwarded_port, guest: 2375, host: 62375
  config.vm.network :forwarded_port, guest: 2376, host: 62376
  config.vm.network :forwarded_port, guest: 60053, host: 60053, protocol: 'udp'
end
