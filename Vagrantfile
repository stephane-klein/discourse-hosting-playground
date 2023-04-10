Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox"
  config.vm.box = "generic/ubuntu2210"
  config.vm.synced_folder '.', '/vagrant/', disabled: false
  config.vm.network "private_network", type: "dhcp"

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.manage_guest = true
  config.hostmanager.aliases = ["forum.example.com"]
end
