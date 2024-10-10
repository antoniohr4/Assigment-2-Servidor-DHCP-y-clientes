# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"

  #server
  config.vm.define "server" do |sv|
    sv.vm.network "private_network", ip: "192.168.56.10"
    sv.vm.network "private_network", ip: "192.168.57.10", virtualbox__intnet: true
    sv.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get upgrade -y
    apt-get install -y isc-dhcp-server
    cp -v /vagrant/dhcpd.conf /etc/dhcp/
    cp -v /vagrant/isc-dhcp-server /etc/default/
    systemctl restart isc-dhcp-server
    SHELL
  end

  config.vm.define "cliente1" do |c1|
    c1.vm.network "private_network",
      type: "dhcp",
      virtualbox__intnet: true
  end

  config.vm.define "cliente2" do |c2|
    c2.vm.network "private_network",
      type: "dhcp",
      mac: "5CA1AB1E0002",
      virtualbox__intnet: true
    
  end

end
