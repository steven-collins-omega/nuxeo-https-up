# Vagrantfile essentially due to Unizin

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

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
    ansible.playbook = "playbook.yml"
  end

end
