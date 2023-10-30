Vagrant.configure("2") do |config|
  config.vm.box = "debian/bullseye64"
  config.vm.hostname = "gp1f4a7blue.fjeclot.ne"

  config.vm.provider "virtualbox" do |v|
    v.name = "gp1f4a7blue"
    v.memory = 2048
    v.cpus = 2
    v.customize ['modifyvm', :id, '--clipboard', 'bidirectional', '--groups', '/GP1']
  end

  config.vm.network "public_network", type: "dhcp", bridge: "Qualcomm_Athereos_QCA61x4A_Wireless_Network_Adapter"
  config.vm.synced_folder "../codi", "/home/vagrant/gp1f4a7/codi"

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update -y
    sudo apt-get install -y aptitude
    sudo apt-get install -y net-tools
    sudo apt-get install -y apt-transport-https ca-certificates curl gnupg2 software-properties-common
    sudo curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
    sudo apt-get update -y
    sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose
    sudo apt-get install -y git unzip zip
    sudo gpasswd -a vagrant docker
    sudo chown -R vagrant:vagrant /home/vagrant/gp1f4a7
    usermod -aG docker vagrant
  SHELL
end