IMAGE_NAME = "debian/stretch64"
N = 2

Vagrant.configure("2") do |config|
    # Because we don't care about security
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 1024
        v.cpus = 2
    end
      
    config.vm.define "master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.100.10"
        master.vm.hostname = "master"

        master.vm.provision "install-docker", type: "ansible" do |ansible|
            ansible.playbook = "install-docker-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.100.10",
            }
        end

        master.vm.provision "disable-swap", type: "ansible" do |ansible|
            ansible.playbook = "disable-swap-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.100.10",
            }
        end

        master.vm.provision "kubelet-kubeadm-kubectl", type: "ansible" do |ansible|
            ansible.playbook = "kubelet-kubeadm-kubectl-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.100.10",
            }
        end

        master.vm.provision "initialize-kubeadm", type: "ansible" do |ansible|
            ansible.playbook = "initialize-kubeadm-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.100.10",
            }
        end

        master.vm.provision "vagrant-user-config", type: "ansible" do |ansible|
            ansible.playbook = "vagrant-user-config-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.100.10",
            }
        end

        master.vm.provision "networking-provider", type: "ansible" do |ansible|
            ansible.playbook = "networking-provider-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.100.10",
            }
        end

        master.vm.provision "join-command", type: "ansible" do |ansible|
            ansible.playbook = "join-command-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.100.10",
            }
        end
    end

    (1..N).each do |i|
        config.vm.define "node-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "192.168.100.#{i + 10}"
            node.vm.hostname = "node-#{i}"

            node.vm.provision "install-docker", type: "ansible" do |ansible|
              ansible.playbook = "install-docker-playbook.yml"
              ansible.extra_vars = {
                  node_ip: "192.168.100.#{i + 10}",
              }
            end

            node.vm.provision "disable-swap", type: "ansible" do |ansible|
              ansible.playbook = "disable-swap-playbook.yml"
              ansible.extra_vars = {
                  node_ip: "192.168.100.#{i + 10}",
              }
            end

            node.vm.provision "kubelet-kubeadm-kubectl", type: "ansible" do |ansible|
              ansible.playbook = "kubelet-kubeadm-kubectl-playbook.yml"
              ansible.extra_vars = {
                  node_ip: "192.168.100.#{i + 10}",
              }
            end

            node.vm.provision "join-nodes", type: "ansible" do |ansible|
              ansible.playbook = "join-nodes-playbook.yml"
              ansible.extra_vars = {
                  node_ip: "192.168.100.#{i + 10}",
              }
            end
        end
    end
end
