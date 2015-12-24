Vagrant.configure(2) do |config|

  config.vm.box = "centos/7"

  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.network :forwarded_port, guest: 443, host: 4430
  config.vm.network :forwarded_port, guest: 3306, host: 33060
  config.vm.network :forwarded_port, guest: 1025, host: 10250
  config.vm.network :forwarded_port, guest: 1080, host: 10800
  config.vm.network :forwarded_port, guest: 6379, host: 63790

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

  config.vm.synced_folder "~/.ssh",
    "/home/vagrant/keys/",
     mount_options: ["dmode=777", "fmode=600"]
  config.vm.synced_folder "../myzanichelli_source_v2",
    "/opt/myzanichelli_source_v2",
     mount_options: ["dmode=777", "fmode=777"]
  config.vm.synced_folder "../myzanichelli_source",
    "/opt/myzanichelli_source",
    mount_options: ["dmode=777", "fmode=777"]

  config.vm.provision :ansible_local do |ansible|
    #ansible.verbose = "v"
    ansible.playbook = "playbook.yml"
    ansible.install = true
    ansible.version = "latest"
  end
end