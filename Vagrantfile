Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/bionic64"
    config.vm.provider "virtualbox" do |vb|
        vb.memory = 4096
        vb.cpus = 2
    end

    config.vm.define "kubernetes" do |dk1|
        dk1.vm.provider "virtualbox" do |vb|
            vb.name= "kubernetes"
            vb.memory = 4096
            vb.cpus = 2
        end
        dk1.vm.network "private_network", ip: "192.168.1.21"
        dk1.vm.network "forwarded_port", guest: 80, host: 8080, protocol: "tcp"
        dk1.vm.provision "shell", inline: "apt-get update"
        dk1.vm.provision "shell", inline: "apt-get install -y docker.io"
        dk1.vm.provision "shell", inline: "systemctl start docker"
        dk1.vm.provision "shell", inline: "systemctl enable docker"
        dk1.vm.provision "shell", inline: "usermod -aG docker vagrant"
        dk1.vm.provision "shell", inline: "curl -LO https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
        dk1.vm.provision "shell", inline: "chmod +x kubectl"
        dk1.vm.provision "shell", inline: "mkdir -p ~/.local/bin"
        dk1.vm.provision "shell", inline: "mv ./kubectl ~/.local/bin/kubectl"
        dk1.vm.provision "shell", inline: "curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64"
        dk1.vm.provision "shell", inline: "sudo install minikube-linux-amd64 /usr/local/bin/minikube"
        dk1.vm.hostname = "kubernetes"
    end
end
