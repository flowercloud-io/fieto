# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

# Require a recent version of vagrant otherwise some have reported errors setting host names on boxes
Vagrant.require_version ">= 1.6.2"

# This stuff is cargo-culted from http://www.stefanwrobel.com/how-to-make-vagrant-performance-not-suck
# Give access to half of all cpu cores on the host. We divide by 2 as we assume
# that users are running with hyperthreads.
host = RbConfig::CONFIG['host_os']
if host =~ /darwin/
  $vm_cpus = (`sysctl -n hw.ncpu`.to_i/2.0).ceil
elsif host =~ /linux/
  $vm_cpus = (`nproc`.to_i/2.0).ceil
else # sorry Windows folks, I can't help you
  $vm_cpus = 2
end

# Give VM 512MB of RAM
$vm_mem = 2048

$provision = <<SCRIPT
  DEBIAN_FRONTEND=noninteractive

  apt-get update
  apt-get install -y build-essential software-properties-common curl htop vim wget
  wget https://github.com/spf13/hugo/releases/download/v0.15/hugo_0.15_linux_amd64.tar.gz -O /tmp/hugo.tar.gz
  tar zxvf /tmp/hugo.tar.gz -C /tmp
  cp /tmp/hugo_0.15_linux_amd64/hugo_0.15_linux_amd64 /usr/local/bin/hugo

  apt-get remove --purge -y chef puppet
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  # Networking
  config.vm.hostname = "flowercloud-fieto"
  config.vm.network "private_network", ip: "33.33.33.31"
  config.vm.network :forwarded_port, host: 1313, guest:1313, auto_correct: true

  # Provider
  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--memory", $vm_mem]
    v.customize ["modifyvm", :id, "--cpus", $vm_cpus]

    # Use faster paravirtualized networking
    v.customize ["modifyvm", :id, "--nictype1", "virtio"]
    v.customize ["modifyvm", :id, "--nictype2", "virtio"]
  end

  # Provisioning
  config.vm.provision :shell, inline: $provision

  # Shared Folders
  config.vm.synced_folder ".", "/home/vagrant/fieto"

end

