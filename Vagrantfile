ssh_port = 22   #use 22 at first time
home_dir="/home/ubuntu"

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.box_url = "ubuntu/xenial64" #https://atlas.hashicorp.com/ubuntu/boxes/xenial64/versions/20160707.0.0/providers/virtualbox.box"

    config.vm.network "private_network", ip: "192.168.33.11"
    config.vm.network "forwarded_port", guest: ssh_port, host: 2223, id: "ssh"

    config.vm.provider "virtualbox" do |vb|
        vb.name = "ubuntu-xenial-16.04-for-ansible-manager"
    end

    config.vm.synced_folder "provision/", home_dir + "/provision" , type: "nfs"
    config.vm.synced_folder "src/", home_dir + "/src" , type: "nfs"

    config.vm.provision "shell", privileged: false, inline: <<-SHELL
        sudo cp ~/provision/cert/*.crt /usr/local/share/ca-certificates/
        sudo update-ca-certificates

        echo "127.0.0.1 `hostname`" | sudo tee -a /etc/hosts

        sudo apt-get -y update

        sudo apt-get -y install python2.7
        #sudo ln -s `which python2.7` /usr/bin/python
        sudo apt-get -y install software-properties-common
        sudo apt-add-repository ppa:ansible/ansible
        sudo apt-get -y update
        sudo apt-get -y install ansible

    SHELL
end
