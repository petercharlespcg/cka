Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
	
  config.vm.define "m1-centos", primary: true do |master|
    master.vm.provider "virtualbox" do |vb|
	  vb.name = "m1-centos"
	  vb.memory = "2048"
	  vb.cpus = 2
  	end
	master.vm.hostname = "m1-centos"
	master.vm.network "private_network", ip: "192.168.20.10"
  end

  NODE_COUNT = 2
  (1..NODE_COUNT).each do |i|
    config.vm.define "c#{i}-centos", autostart: false do |node|
      node.vm.provider "virtualbox" do |vb|
	    vb.name = "c#{i}-centos"
	    #vb.memory = "1024"
	    vb.cpus = 1
	  end
	  node.vm.hostname = "c#{i}-centos"
	  node.vm.network "private_network", ip: "192.168.20.#{i + 10}"
    end
  end
end
