# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
  # Set box configuration
  config.vm.box = "lucid32"
  config.vm.box_url = "http://files.vagrantup.com/lucid32.box"

  config.vm.host_name = "vbox5"

  # Assign this VM to a host-only network IP, allowing you to access it via the IP.
  config.vm.network :bridged
  config.vm.network :hostonly, "192.168.56.5"

  #config.vm.share_folder "netbeans", "/srv/netbeans", "/Users/diego/NetBeansProjects/" , :nfs=>true
  config.vm.share_folder "netbeans", "/srv/netbeans", "/Users/diego/NetBeansProjects/", :owner=> 'vagrant', :group=>'www-data', :extra => 'dmode=775,fmode=775'

  config.vm.share_folder "zendstudio", "/srv/zendstudio", "/Users/diego/Zend/workspaces/DefaultWorkspace/"

  # Enable provisioning with chef solo, specifying a cookbooks path (relative
  # to this Vagrantfile), and adding some recipes and/or roles.
  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"
    chef.data_bags_path = "data_bags"
    chef.add_recipe "vagrant_main"

    chef.json.merge!({
      "mysql" => {
        "server_root_password" => "vagrant",
        "bind_address" => "0.0.0.0"
      },
      "oh_my_zsh" => {
        :users => [
          {
            :login => 'vagrant',
            :theme => 'blinks',
            :plugins => ['git', 'gem']
          }
        ]
      }
    })
  end
end
