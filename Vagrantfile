BOX_IMAGE = "dgilliam-centos7"
NODE_COUNT = 2

Vagrant.configure("2") do |config|
  config.vm.define "master01" do |subconfig|
    subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "master"
    subconfig.vm.network "private_network", ip: "10.0.0.10"
    subconfig.vm.provision "ansible" do |ansible|
      ansible.playbook = "masters.yml"
      ansible.inventory_path = "inventory"
    end
  end

  # Create node01 and node02
  (1..NODE_COUNT).each do |i|
    config.vm.define "node0#{i}" do |subconfig|
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.hostname = "node0#{i}"
      if i == 1
        ip = "10.0.0.11"
      elsif i == 2
        ip = "10.0.0.12"
      end
      subconfig.vm.network "private_network", ip: ip
      subconfig.vm.provision "ansible" do |ansible|
        ansible.playbook = "nodes.yml"
        ansible.inventory_path = "inventory"
      end
    end
  end

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false
    # Customize the amount of memory on the VM:
    vb.memory = "2048"
    vb.cpus = 2
  end
end
