# Install required plugins
required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/bionic64"
    app.vm.network "private_network", ip: "192.168.10.100"
    app.hostsupdater.aliases = ["development.local"]
    app.vm.synced_folder "app", "/home/ubuntu/app"
    app.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
    end
    app.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
  end


  config.vm.define "db" do |db|
    db.vm.box = "ubuntu/bionic64"
    db.vm.network "private_network", ip: "192.168.10.150"
    db.hostsupdater.aliases = ["database.local"]
    db.vm.synced_folder "environment/db", "/home/ubuntu/environment"
    db.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
    end

    db.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
  end

  config.vm.define "jenkinsslave" do |jenkinsslave|
    jenkinsslave.vm.box = "ubuntu/bionic64"
      jenkinsslave.vm.network "private_network", ip: "192.168.10.200"
    jenkinsslave.hostsupdater.aliases = ["localhost:8080 "]
    jenkinsslave.vm.synced_folder "environment/jenkinsslave", "/home/ubuntu/jenkins"
    jenkinsslave.vm.provision "shell", path: "environment/jenkinsslave/provision.sh", privileged: false
    jenkinsslave.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
  end
end
