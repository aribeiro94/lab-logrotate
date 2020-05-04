$packages = <<-SCRIPT
sudo yum install epel-release -y
sudo yum install nc telnet vim htop ansible git tree -y
grep 192.168.254.204 /etc/hosts || echo "192.168.254.204 centos7" >> /etc/hosts
grep 192.168.254.205 /etc/hosts || echo "192.168.254.204 opensuse15" >> /etc/hosts
SCRIPT

Vagrant.configure("2") do |config|
  
    config.vm.define "ansible" do |ansible|
        ansible.vm.box = "centos/7"
        ansible.vm.hostname = "ansible"
        ansible.vm.network "private_network", ip: "192.168.254.203"
        ansible.vm.provision "shell", inline: $packages
        #ansible.vm.provision "file", source: "~/path/to/host/folder", destination: "$HOME/remote/newfolder"
        ansible.vm.provider "virtualbox" do |v|
            v.gui = false
            v.memory = 1024
            v.cpus = 2
        end
        
    end
  
    config.vm.define "centos7" do |target_centos|
        target_centos.vm.box = "centos/7"
        target_centos.vm.hostname = "centos7"
        target_centos.vm.network "private_network", ip: "192.168.254.204"
    end

    config.vm.define "opensuse15" do |target_opensuse|
        target_opensuse.vm.box = "generic/opensuse15"
        target_opensuse.vm.hostname = "opensuse15"
        target_opensuse.vm.network "private_network", ip: "192.168.254.205"
    end    
  end
  
