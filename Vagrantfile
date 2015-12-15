Vagrant.configure(2) do |config|

  config.vm.box = "centos/7"

  config.vm.network :forwarded_port, guest: 80, host: 80
  config.vm.network :forwarded_port, guest: 443, host: 443
  config.vm.network :forwarded_port, guest: 3306, host: 3306

  config.vm.network :private_network, ip: "192.168.10.10", netmask: "255.255.255.0"

  config.vm.box = "myz-centos7"
  config.vm.box_url = "https://github.com/holms/vagrant-centos7-box/releases/download/7.1.1503.001/CentOS-7.1.1503-x86_64-netboot.box"

  config.hostmanager.aliases = %w(admin-my.zanichelli.local cdn-my.zanichelli.local my.zanichelli.local api-my.zanichelli.local dev.myzanichelli.local)
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  config.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.customize ["modifyvm", :id, "--memory", "2048"]
      vb.customize ["modifyvm", :id, "--cpus", "1"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  config.vm.synced_folder "../../Documenti/myzanichelli_source_v2",
    "/vagrant/myzanichelli_source_v2",
     mount_options: ["dmode=777", "fmode=777"]
  config.vm.synced_folder "../../Documenti/myzanichelli_source",
    "/vagrant/myzanichelli_source",
    mount_options: ["dmode=777", "fmode=777"]

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbook.yml"
  end
end