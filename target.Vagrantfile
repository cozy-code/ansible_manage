ssh_port = 22   #use 22 at first time
home_dir="/home/ubuntu"

# mkdir ansible_target
# cd ansible_target
# ln -s path/to/target.Vagrantfile ./Vagrantfile

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.box_url = "ubuntu/xenial64" #https://atlas.hashicorp.com/ubuntu/boxes/xenial64/versions/20160707.0.0/providers/virtualbox.box"

    config.vm.network "private_network", ip: "192.168.33.12"
    config.vm.network "forwarded_port", guest: ssh_port, host: 2224, id: "ssh"

    config.vm.provider "virtualbox" do |vb|
        vb.name = "ubuntu-xenial-16.04-for-ansible-target"
        vb.memory = "512"
        vb.cpus = 1

        #vb.memory = "1024"
        #vb.cpus = 2
    end

end
