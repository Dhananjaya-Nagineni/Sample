# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "Jenkins" do |vm1|
    vm1.vm.box = "generic/oracle8"
	  vm1.vm.network "private_network", ip: "192.168.57.12"
	  vm1.vm.network "public_network"
    vm1.vm.hostname = "Ora"
    vm1.disksize.size = '50GB'
    vm1.vm.synced_folder ".", "/vagrant"
    
	  vm1.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
=begin
    vm1.vm.provision "shell", inline: <<-SHELL
    sudo su -

uname -a
cat /etc/os-release

# Check RAM & Swap
grep MemTotal /proc/meminfo
grep SwapTotal /proc/meminfo

# Adjust Swap to 4GB
sudo swapoff -a
sudo cp /etc/fstab /etc/fstab.bak
sudo sed -i '/swap/d' /etc/fstab
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile swap swap defaults 0 0' | sudo tee -a /etc/fstab
swapon --show
grep SwapTotal /proc/meminfo

# Check CPU & Disk
lscpu
df -h

# Install prerequisites
yum install -y oracle-database-preinstall-19c

# Verify kernel parameters
sudo sysctl -p

# Verify shell limits
ulimit -a

# Create/verify groups, user, and set password
getent group oinstall
getent group dba
id oracle
passwd oracle
oracle

# Create required directories
sudo mkdir -p /u01/app/oracle/product/19.0.0/dbhome_1
sudo mkdir -p /u01/app/oraInventory
sudo mkdir -p /u02/oradata
sudo mkdir -p /u02/fra
sudo mkdir -p /u03/oracle/export

# Set ownership and permissions
sudo chown -R oracle:oinstall /u01 /u02 /u03
sudo chmod -R 775 /u01 /u02 /u03

# Verify directories, permissions, ownership
ls -ld /u01/app/oracle
ls -ld /u01/app/oracle/product/19.0.0/dbhome_1
ls -ld /u01/app/oraInventory
ls -ld /u02/oradata
ls -ld /u02/fra
ls -ld /u03/oracle/export
find /u01 /u02 /u03 -type d -exec ls -ld {} \;

# Set Oracle environment for oracle user
sudo su - oracle
oracle
vi ~/.bash_profile

# Add:
export ORACLE_BASE=/u01/app/oracle
export ORACLE_HOME=$ORACLE_BASE/product/19.0.0/dbhome_1
export ORACLE_INVENTORY=/u01/app/oraInventory
export ORACLE_SID=ORCL
export PATH=$PATH:$ORACLE_HOME/bin
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
export CLASSPATH=$ORACLE_HOME/jlib:$ORACLE_HOME/rdbms/jlib

source ~/.bash_profile

wget --no-check-certificate --content-disposition "https://download.oracle.com/otn/linux/oracle19c/190000/LINUX.X64_193000_db_home.zip?AuthParam=1773405847_75d2a4894518d00c35e51601410351aa"

mv LINUX.X64_193000_db_home.zip?AuthParam=1773405847_75d2a4894518d00c35e51601410351aa LINUX.X64_193000_db_home.zip
cp * $ORACLE_HOME
cd $ORACLE_HOME
unzip LINUX.X64_193000_db_home.zip


    SHELL
=end    
   end
  end

  config.vm.define "web01" do |web01|
    web01.vm.box = "geerlingguy/centos7"
	web01.vm.network "private_network", ip: "192.168.10.13"
        web01.vm.hostname = "web01"
  end
  
  config.vm.define "web02" do |web02|
    web02.vm.box = "geerlingguy/centos7"
	web02.vm.network "private_network", ip: "192.168.10.14"
        web02.vm.hostname = "web02"
  end

   config.vm.define "web03" do |web03|
    web03.vm.box = "ubuntu/bionic64"
        web03.vm.network "private_network", ip: "192.168.10.15"
        web03.vm.hostname = "web03"
  end
end

  # config.vm.box_check_update = false
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"
  # config.vm.synced_folder "../data", "/vagrant_data"
  # config.vm.synced_folder ".", "/vagrant", disabled: true
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL


