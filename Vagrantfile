Vagrant.configure(2) do |config|
  config.vm.box = "windows-2016-amd64" # see https://github.com/rgl/windows-2016-vagrant

  config.vm.provider "libvirt" do |lv, config|
    lv.memory = 4096
    lv.cpus = 2
    lv.cpu_mode = "host-passthrough"
    # lv.nested = true
    lv.keymap = "pt"
    config.vm.synced_folder ".", "/vagrant", type: "smb", smb_username: ENV["USER"], smb_password: ENV["VAGRANT_SMB_PASSWORD"]
  end

  config.vm.provider "virtualbox" do |vb|
    vb.linked_clone = true
    vb.memory = 4096
    vb.cpus = 2
    vb.customize ["modifyvm", :id, "--vram", 64]
    vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
    vb.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]
  end

  config.vm.provision "shell", inline: "$env:chocolateyVersion='0.10.11'; iwr https://chocolatey.org/install.ps1 -UseBasicParsing | iex", name: "Install Chocolatey"
  config.vm.provision "shell", path: "Vagrantfile-locale.ps1"
  config.vm.provision "shell", path: "Vagrantfile-provision.ps1"
  config.vm.provision "shell", path: "Vagrantfile-provision-kibana.ps1"
end