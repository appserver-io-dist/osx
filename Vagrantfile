# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Box name and location
  config.vm.box = "${vagrant-box.name}"
  config.vm.box_url = "${vagrant-box.baseurl}/${vagrant-box.name}.box"

  # Basic network configuration
  config.vm.base_mac = "080027BE1722"
  # Required for AFP to work, and AFP is required as Mac OSX is missing VB guest additions
  config.vm.network "forwarded_port", host: ${vagrant.afp.local-port}, guest: 548

  # Block vagrant driven folder syncing
  config.vm.synced_folder "${temp.dir}", "${vagrant.basedir}", disabled: true

  # Extend the timeout for initial connection
  config.vm.boot_timeout = 600
  config.ssh.insert_key = false

  config.vm.provider "virtualbox" do |vb|
    host = RbConfig::CONFIG['host_os']

    # Give VM 2Gb system memory & access to 2 cpu cores on the host
    vb.cpus = 2
    vb.memory = 2048
  end

  config.vm.define :"${vagrant-box.name}" do |t|
    end
end
