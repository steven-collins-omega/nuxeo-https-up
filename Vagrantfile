# Vagrantfile essentially due to Unizin

# 1.8 needed for ansible-galaxy features
Vagrant.require_version ">= 1.8.0"

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

  # ensure everyone is using the same box; we only update the version
  # when we make a conscious decision to do so
  config.vm.box_version = "= 20160222.0.0"

  # essential idea of following comes from juanje on github:
  # https://gist.github.com/juanje/3797297
  # This is like using vagrant-cachier except much more lightweight
  # and more likely to work cross-(host-)platform.
  config.vm.synced_folder ".apt-cache", "/var/cache/apt/archives",
                          create: true, owner: "root", group: "root"

  config.vm.hostname = "nuxeo.local"
  config.vm.network "private_network", ip: "10.10.10.10"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end

  config.vm.provision "ansible" do |ansible|
    nuxeo_dir = "nuxeo-tools-cloud/ansible/nuxeo/"
    ansible.playbook = nuxeo_dir + "deploy-cloud.yml"
    ansible.groups = {
      "nuxeo" => ["default"],
      "db"    => ["default"],
      "https" => ["default"],
      "cloud:children" => ["nuxeo", "db", "https"]
    }
    # ansible.tags = ["https"]
    # ansible.verbose = "vvv"
  end

end
