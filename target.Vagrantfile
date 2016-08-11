ssh_port = 22   #use 22 at first time
ssh_port = 4126   #use alt port after ansible
home_dir="/home/ubuntu"

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.box_url = "ubuntu/xenial64" #https://atlas.hashicorp.com/ubuntu/boxes/xenial64/versions/20160707.0.0/providers/virtualbox.box"

    # login before ansible> ssh ansible@192.168.33.12
    # login after  ansible> ssh ansible@192.168.33.12 -p 4126 -i ../ansible_manage/src/playbooks_xenial64/keys/id_rsa_ansible

    config.vm.network "private_network", ip: "192.168.33.12"
    config.vm.network "forwarded_port", guest: ssh_port, host: 2224, id: "ssh"


    config.vm.provider "virtualbox" do |vb|
        vb.name = "ubuntu-xenial-16.04-for-ansible-target"
    end

    # create ansible working user
    config.vm.provision "shell", privileged: false, inline: <<-SHELL
        sudo adduser --disabled-password --gecos "" ansible
        echo ansible:ansiblepassword | sudo chpasswd
        sudo gpasswd -a ansible sudo
    SHELL

    config.vm.synced_folder "src/", "/home/ansible/src" , type: "nfs"

end
