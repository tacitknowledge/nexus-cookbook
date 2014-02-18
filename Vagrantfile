Vagrant.configure("2") do |config|

  config.vm.hostname = "nexus-berkshelf"

  # Requires the vagrant-berkshelf plugin
  config.berkshelf.enabled = true
  config.omnibus.chef_version = '11.6.2'

  config.vm.box = "centos64"
  config.vm.box_url = "https://storage.tacitknowledge.com/tk-storage/common/public/software/vagrant_boxes/centos64-virtualbox.box"
  config.vm.network :private_network, ip: "192.168.33.110"
  #config.vm.network :forwarded_port, guest: 8081, host: 8081
  #config.vm.network :forwarded_port, guest: 8443, host: 8443

  config.vm.provision :chef_solo do |chef|
    chef_dir = File.join(Dir.home, ".chef")
    chef.data_bags_path = File.join(chef_dir, "data_bags")
    # chef.encrypted_data_bag_secret_key_path = File.join(chef_dir, "encrypted_data_bag_secret")

    chef.json = {
      :java => {
        :install_flavor => "oracle",
        :jdk_version => "7",
        :oracle => {
          :accept_oracle_download_terms => true
          }
        },
      :nexus => {
        :cli => {
          :ssl => {
            :verify => false
          }
        },
        :app_server_proxy => {
          :use_self_signed => true
        }
      }
    }

    chef.run_list = [
      "recipe[nexus::default]"
    ]
  end
end
