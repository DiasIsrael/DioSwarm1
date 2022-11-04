machines = {
  "master" => {"memory" => "1024", "cpu" => "1", "ip" => "100", "image" => "ubuntu/focal64"},
  "node01" => {"memory" => "1024", "cpu" => "1", "ip" => "201", "image" => "ubuntu/focal64"},
  "node02" => {"memory" => "1024", "cpu" => "1", "ip" => "202", "image" => "ubuntu/focal64"},
  "node03" => {"memory" => "1024", "cpu" => "1", "ip" => "203", "image" => "ubuntu/focal64"}
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
      machine.vm.network "private_network", ip: "10.0.0.#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]

      end
      machine.vm.provision "shell", path: "dockerinstall.sh"

      if "#{name}" =="master"
        machine.vm.provision "shell", path: "master.sh"
      else
        machine.vm.provision "shell", path: "worker.sh"
      end

    end
  end
  
end
