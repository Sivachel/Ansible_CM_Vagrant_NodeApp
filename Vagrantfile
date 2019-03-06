Vagrant.configure(2) do |config|
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/xenial64"
    app.vm.network "private_network", ip: "192.168.10.120"
    app.vm.network "forwarded_port", guest: 3000, host: 8080
    app.vm.provision "ansible_local" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "app.yml"
      ansible.become = true
    end
  end

#   config.vm.define "app02" do |app02|
#     app02.vm.box = "ubuntu/xenial64"
#     app02.vm.network "private_network", ip: "192.168.10.140"
#     app02.vm.provision "ansible_local" do |ansible|
#       ansible.verbose = "v"
#       ansible.playbook = "webserver.yml"
#       ansible.become = true
#     end
#   end
end
