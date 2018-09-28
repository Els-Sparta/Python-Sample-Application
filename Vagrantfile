required_plugins = ["vagrant-berkshelf", "vagrant-hostsupdater"]
required_plugins.each do |plugin|
    unless Vagrant.has_plugin? plugin
      puts "installing vagrant plugin #{plugin}"
      Vagrant::Plugin::Manager.instance.install_plugin plugin
      puts "installed vagrant plugin #{plugin}"
    end
end


Vagrant.configure("2") do |config|
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/xenial64"
    app.vm.network "private_network", ip: "192.168.10.100"
    app.vm.synced_folder "../Python-Sample-Application", "/home/ubuntu/"
    app.vm.provision "chef_solo" do |chef|
      chef.add_recipe "nginx::default"
      chef.add_recipe "python::default"
    end
  end
end
