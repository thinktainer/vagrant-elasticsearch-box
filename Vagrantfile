# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "opscode_ubuntu-12.04"
  config.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/vmware/opscode_ubuntu-12.04_chef-provisionerless.box"
  config.vm.network :forwarded_port, guest: 9200, host: 9200
  config.vm.network :forwarded_port, guest: 9300, host: 9300
  config.vm.network :forwarded_port, guest: 5601, host: 5601
  config.vm.network "private_network", ip: "192.168.165.128"
  config.vm.provision "shell", path: "install-puppet.sh"
  config.vm.provision :puppet, :module_path => "modules" do |puppet|
    puppet.manifests_path = "manifests"
    puppet.manifest_file  = "default.pp"
  end
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--cpus", "2"]
    v.customize ["modifyvm", :id, "--memory", "1024"]
  end
  config.vm.provider "vmware_fusion" do |v, override|
    override.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/vmware/opscode_ubuntu-12.04_chef-provisionerless.box"
    v.vmx["memsize"] = "1024"
    v.vmx["numvcpus"] = 1
    override.vm.box = "opscode_ubuntu-12.04"
    v.vmx["ethernet1.present"] = "TRUE"
    v.vmx["ethernet1.connectionType"] = "hostonly"
    v.vmx["ethernet1.virtualDev"] = "e1000"
    v.vmx["ethernet1.wakeOnPcktRcv"] = "FALSE"
  end
end
