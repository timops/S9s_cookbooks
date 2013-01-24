require 'berkshelf/vagrant'


Vagrant::Config.run do |config|

  #config.vm.forward_port 3000, 3000

  config.vm.define :control do |ctl_config|
    ctl_config.vm.box = "opscode-ubuntu-12.04"
    ctl_config.vm.host_name = "control.s9.local"                                                                                                                                  
    ctl_config.vm.network :hostonly, '192.168.122.9'
    ctl_config.vm.provision :chef_client do |chef|
      chef.chef_server_url = "https://api.opscode.com/organizations/persuse"

      chef.validation_client_name = "persuse-validator"
      chef.validation_key_path = "persuse-validator.pem"
      chef.client_key_path = "/etc/chef/client.pem"

      chef.environment = "S9"

      #chef.add_recipe("apache2")
      #chef.add_role("database")
      #chef.run_list = [
      #]

      #chef.node_name = "#{user}-vagrant"
      #chef.log_level = :info
    end
  end

  3.times do |i|  
    config.vm.define "db-#{i}" do |db_cfg|
     db_cfg.vm.host_name = "db-#{i}.s9.local"                                                                                                                                  
     db_cfg.vm.network :hostonly, "192.168.122.1#{i}"
     db_cfg.vm.box = "opscode-ubuntu-12.04"
     db_cfg.vm.provision :chef_client do |chef|
       chef.chef_server_url = "https://api.opscode.com/organizations/persuse"

       chef.validation_client_name = "persuse-validator"
       chef.validation_key_path = "persuse-validator.pem"
       chef.client_key_path = "/etc/chef/client.pem"
      
       chef.environment = "S9"

       chef.run_list = [
         "role[cc_galera]"
       ]
     end
    end 
  end

=begin
   config.vm.define :db_1 do |db_cfg|
     db_cfg.vm.box = "opscode-ubuntu-12.04"
     db_cfg.vm.provision :chef_client do |chef|
       chef.chef_server_url = "https://api.opscode.com/organizations/persuse"

       chef.validation_client_name = "persuse-validator"
       chef.validation_key_path = "persuse-validator.pem"
       chef.client_key_path = "/etc/chef/client.pem"
     end
   end 

   config.vm.define :db_2 do |db_cfg|
     db_cfg.vm.box = "opscode-ubuntu-12.04"
     db_cfg.vm.provision :chef_client do |chef|
       chef.chef_server_url = "https://api.opscode.com/organizations/persuse"

       chef.validation_client_name = "persuse-validator"
       chef.validation_key_path = "persuse-validator.pem"
       chef.client_key_path = "/etc/chef/client.pem"
     end
   end 
=end

end
