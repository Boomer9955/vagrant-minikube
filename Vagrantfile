IMAGE_NAME = "centos/7" 
NODE_NAME = "centos-minikube"

Vagrant.configure("2") do |config|
    #config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
    end
    
    config.ssh.insert_key = true
    config.ssh.forward_agent = true

    config.vm.network "forwarded_port",
    guest: 8001,
    host:  8001,
    auto_correct: true

    config.vm.network "forwarded_port",
    guest: 30000,
    host:  30000,
    auto_correct: true

    config.vm.network "forwarded_port",
    guest: 8443,
    host:  8443,
    auto_correct: true

    config.vm.define NODE_NAME do |master|     

        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.30.120"
        master.vm.hostname = NODE_NAME
        master.vm.provision "ansible_local" do |ansible|
            ansible.compatibility_mode = "2.0"
            ansible.playbook = "install-minikube.yaml"
            ansible.extra_vars = {
                node_ip: "192.168.30.120",
            }
        end
    end
end