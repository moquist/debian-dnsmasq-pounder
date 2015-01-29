VAGRANTFILE_API_VERSION = "2"

Vagrant.require_version ">= 1.6.3"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "debian-dnsmasq-pounder"

  config.vm.box = "yungsang/boot2docker"

  config.vm.synced_folder ".", "/vagrant"

  # This makes --provision indempotent.
  config.vm.provision "shell", inline: <<-SHELL
    docker stop dnsmasq || true
    docker rm dnsmasq || true
  SHELL

  config.vm.provision :docker do |d|
    d.build_image "/vagrant/vmfiles",
      args: "-t moquist/debian-dnsmasq-pounder"
    d.run "dnsmasq",
      image: "moquist/debian-dnsmasq-pounder",
      args: "-p 60053:60053/udp -v /vagrant/vmfiles/dnsmasq-conf:/opt/dnsmasq-conf:ro",
      cmd: "/usr/sbin/dnsmasq -C /opt/dnsmasq-conf/dnsmasq.conf -d"
  end

  config.vm.network :forwarded_port, guest: 2375, host: 62375
  config.vm.network :forwarded_port, guest: 60053, host: 60053, protocol: 'udp'
end
