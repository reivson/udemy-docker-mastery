# -*- mode: ruby -*-
# vi: set ft=ruby  :

machines = {
  "swarm1" => {"memory" => "1536", "cpu" => "2", "ip" => "10", "image" => "ubuntu/bionic64"},
  "swarm2" => {"memory" => "1536", "cpu" => "2", "ip" => "20", "image" => "ubuntu/bionic64"},
  "swarm3"  => {"memory" => "1536", "cpu" => "2", "ip" => "30", "image" => "ubuntu/bionic64"}
}

Vagrant.configure("2") do |config|

  config.vm.box_check_update = false
  config.vm.boot_timeout = 600
  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}.4labs.example"
      machine.vm.network "private_network", ip: "10.10.25.#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        vb.customize ["modifyvm", :id, "--groups", "/Docker-DCA"]
      end
    end
  end
  config.vm.provision "shell", path: "script.sh"
end
