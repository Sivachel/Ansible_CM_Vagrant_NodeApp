required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
   unless Vagrant.has_plugin? (plugin)
     #Uses vagrant plugin manager to install plugin, which will automatically refresh plugin list
     puts "Installing vagrant plugin #{plugin}"
     Vagrant::Plugin::Manager.instance.install_plugin plugin
     puts "Installed vagrant plugin #{plugin}"
   end
end

Vagrant.configure(2) do |config|
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/xenial64"
    app.vm.network "private_network", ip: "192.168.10.120"
    app.hostsupdater.aliases = ["development.local"]
    # app.vm.network "forwarded_port", guest: 3000, host: 8080
    app.vm.provision "ansible_local" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "app.yml"
      ansible.become = true
    end
  end

  config.vm.define "mongo" do |mongo|
    mongo.vm.box = "ubuntu/xenial64"
    mongo.vm.network "private_network", ip: "192.168.10.140"
    mongo.hostsupdater.aliases = ["database.local"]
    mongo.vm.provision "ansible_local" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "mongo.yml"
      ansible.become = true
    end
  end
end
