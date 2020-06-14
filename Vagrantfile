# -*- mode: ruby -*-
# vim: set ft=ruby :
# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
:inetRouter => {
        :box_name => "centos/7",
        #:public => {:ip => '10.10.10.1', :adapter => 1},
        :net => [
                   {ip: '192.168.255.1', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "router-net"},
                   {ip: '192.168.255.3', adapter: 3, netmask: "255.255.255.252", virtualbox__intnet: "router-net"},
                ]
  },
  :centralRouter => {
        :box_name => "centos/7",
        :net => [
                   {ip: '192.168.255.2', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "router-net"},
                   {ip: '192.168.255.4', adapter: 3, netmask: "255.255.255.252", virtualbox__intnet: "router-net"},
                   {ip: '192.168.0.1', adapter: 4, netmask: "255.255.255.240", virtualbox__intnet: "dir-net"},
                   {ip: '192.168.0.33', adapter: 5, netmask: "255.255.255.240", virtualbox__intnet: "hw-net"},
                   {ip: '192.168.0.65', adapter: 6, netmask: "255.255.255.192", virtualbox__intnet: "mgt-net"},
                   {ip: '192.168.253.1', adapter: 7, netmask: "255.255.255.252", virtualbox__intnet: "o2-net"},
                   {ip: '192.168.254.1', adapter: 8, netmask: "255.255.255.252", virtualbox__intnet: "o1-net"},
                ]
  },
  
  :office1Router => {
        :box_name => "centos/7",
        :net => [
                   {ip: '192.168.254.2', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "o1-net"},
                   {ip: '192.168.2.1', adapter: 3, netmask: "255.255.255.192", virtualbox__intnet: "dev1-net"},
                   {ip: '192.168.2.65', adapter: 4, netmask: "255.255.255.192", virtualbox__intnet: "test1-net"},
                   {ip: '192.168.2.129', adapter: 5, netmask: "255.255.255.192", virtualbox__intnet: "man1-net"},
                   {ip: '192.168.2.193', adapter: 6, netmask: "255.255.255.192", virtualbox__intnet: "hw1-net"}
                ]
  },

  :testServer1 => {
        :box_name => "centos/7",
        :net => [
                   {ip: '192.168.2.2', adapter: 2, netmask: "255.255.255.192", virtualbox__intnet: "dev1-net"},
                   {ip: '10.10.10.1', adapter: 3, netmask: "255.255.255.0", virtualbox__intnet: "testLAN"}
                ]
  },

  :testServer2 => {
        :box_name => "centos/7",
        :net => [
                   {ip: '192.168.2.3', adapter: 2, netmask: "255.255.255.192", virtualbox__intnet: "dev1-net"},
                   {ip: '10.10.10.1', adapter: 3, netmask: "255.255.255.0", virtualbox__intnet: "testLAN"}
                ]
  },

  :testClient1 => {
        :box_name => "centos/7",
        :net => [
                   {ip: '192.168.2.4', adapter: 2, netmask: "255.255.255.192", virtualbox__intnet: "dev1-net"},
                   {ip: '10.10.10.254', adapter: 3, netmask: "255.255.255.0", virtualbox__intnet: "testLAN"}
                ]
  },
  
  :testClient2 => {
        :box_name => "centos/7",
        :net => [
                   {ip: '192.168.2.5', adapter: 2, netmask: "255.255.255.192", virtualbox__intnet: "dev1-net"},
                   {ip: '10.10.10.254', adapter: 3, netmask: "255.255.255.0", virtualbox__intnet: "testLAN"}
                ]
  },

}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

    config.vm.provision "ansible" do |ansible|
      #ansible.verbose = "vvvvv"
      ansible.playbook = "playbook.yml"
      ansible.become = "true"
    end

    config.vm.define boxname do |box|

        box.vm.box = boxconfig[:box_name]
        box.vm.host_name = boxname.to_s

        boxconfig[:net].each do |ipconf|
          box.vm.network "private_network", ipconf
        end
        
        if boxconfig.key?(:public)
          box.vm.network "public_network", boxconfig[:public]
        end

        box.vm.provision "shell", inline: <<-SHELL
          mkdir -p ~root/.ssh
                cp ~vagrant/.ssh/auth* ~root/.ssh
        SHELL
        
      end

  end
  
end

