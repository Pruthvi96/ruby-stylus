# -*- mode: ruby -*-
# vi: set ft=ruby :

NAME = "ruby-stylus"
FQDN = "#{NAME}.example.com"

Vagrant.configure("2") do |config|
  # "trusty" is 14.04
  config.vm.box       = "trusty64"
  config.vm.box_url   = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  # Use the normal insecure key
  # https://github.com/mitchellh/vagrant/issues/2608
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id,
      # Basics.
      "--name",       NAME,
      "--memory",     4096,
      # I/O APIC must be enabled to support a multi-core guest.
      "--cpus",       4,
      "--ioapic",     "on",
      # Enable native host virtualization features (yields better performance).
      "--pae",        "on",
      "--hwvirtex",   "on",
      "--largepages", "on",
      "--vtxvpid",    "on",
      # This causes the virtual machine to proxy DNS requests through the host
      # via NAT. Without this, the default resolver on the guest will introduce
      # a 5 second latency on every HTTP request... which is a real downer.
      "--natdnshostresolver1", "on"
    ]
  end

  config.vm.hostname = FQDN

  # Ruby dev box by forgecrafted
  # https://github.com/forgecrafted/vagrant-provision-ruby
  config.vm.provision "shell", inline: "curl -fsS https://raw.githubusercontent.com/forgecrafted/vagrant-provision-ruby/master/script | bash"
end

#
# DONT FORGET!
#
# Force update VirtualBox Guest Additions
# Run the following command inside same directory as Vagrantfile
# Must be done once on your dev system
#
#   vagrant plugin install vagrant-vbguest
#
