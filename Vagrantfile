# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    # Configure the actual windows machine
    config.vm.define "${vagrant-box.name}" do |osx|

        # Basic default configuration used for intial setup of box.
        # Please use if packaged boxes are unavailable or unwelcome
        # osx.vm.box = "chef/osx-${target-os.version}"
        # osx.vm.box_url = "https://vagrantcloud.com/chef/boxes/osx-${target-os.version}"

        # Box name and location
        osx.vm.box = "${vagrant-box.name}"
        osx.vm.box_url = "${vagrant-box.baseurl}/${vagrant-box.name}.box"

        # Basic network configuration
        osx.vm.base_mac = "080027BE1722"

        # Share some needed folders
        osx.vm.synced_folder "${temp.dir}", "${vagrant.basedir}", type: "rsync"
        osx.vm.synced_folder "${build.dir}", "${vagrant-build.dir}", type: "rsync"
        osx.vm.synced_folder "${reports.dir}", "${vagrant-reports.dir}", type: "rsync"
        osx.vm.synced_folder "${src.dir}", "${vagrant-src.dir}", type: "rsync"

        # Extend the timeout for initial connection
        osx.vm.boot_timeout = 600

        # Without guest additions we cannot change the insecure key
        osx.ssh.insert_key = false

        # Make some provider specific configuration changes
        osx.vm.provider "virtualbox" do |vb|
            host = RbConfig::CONFIG['host_os']

            # Give VM 2Gb system memory & access to 2 cpu cores on the host
            vb.customize ["modifyvm", :id, "--memory", "2048"]
            vb.customize ["modifyvm", :id, "--cpus", "2"]
            vb.customize ["modifyvm", :id, "--cpuexecutioncap", "90"]
        end
    end
end
