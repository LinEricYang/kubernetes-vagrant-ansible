# -*- mode: ruby -*-
# # vi: set ft=ruby :

# Only tested on vagrant 1.9.4
Vagrant.require_version ">= 1.9.4"

proxy = ""
no_proxy = "localhost,127.0.0.1,192.168.33.11,192.168.33.12,192.168.33.13"

Vagrant.configure(2) do |config|

  (1..3).each do |i|
    config.vm.define "k8s-node#{i}" do |n|

      n.vm.box = "ubuntu/xenial64"
      n.vm.box_check_update = false
      n.vm.hostname = "k8s-node#{i}"
      n.ssh.forward_agent = true

      n.vm.network "private_network", ip: "192.168.33.#{10+i}", netmask: "255.255.255.0"

      n.vm.provider "virtualbox" do |v|
        v.name = "k8s-node#{i}"
        v.gui = false
        v.memory = 2048
      end

      n.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.force_remote_user = true
        ansible.extra_vars = {
          proxy_needed: if proxy then true else false end,
          proxy_env: {
            http_proxy: proxy,
            https_proxy: proxy,
            no_proxy: no_proxy,
            HTTP_PROXY: proxy,
            HTTPS_PROXY: proxy,
            NO_PROXY: no_proxy
          }
        }
        if i == 1
          ansible.playbook = "provisioning/k8s-master.yml"
        else
          ansible.playbook = "provisioning/k8s-worker.yml"
        end
      end
      # n.vm.provision :shell, path: "scripts/bootstrap_ansible.sh"
      # if i == 1
      #   n.vm.provision :shell, inline: "PYTHONUNBUFFERED=1 ansible-playbook /vagrant/ansible/k8s-master.yml -c local"
      # else
      #   n.vm.provision :shell, inline: "PYTHONUNBUFFERED=1 ansible-playbook /vagrant/ansible/k8s-worker.yml -c local"
      # end
    end
  end
end
