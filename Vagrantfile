boxes=[
  {
    :hostname => "security-test-vm1",
    :ip => "192.168.100.10",
    :box => "ubuntu/trusty64",
    :ram => 4096,
    :cpu => 2,
    :playbook => "hosts_site.yml"
  },

]

Vagrant.configure(2) do |config|
   boxes.each do |machine|
      config.vm.define machine[:hostname] do |node|
         node.vm.box = machine[:box]
         node.vm.hostname = machine[:hostname]
         node.vm.network "private_network", ip: machine[:ip]
         node.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
         end
      end
      config.vm.provision "ansible" do |ansible|
        ansible.playbook = machine[:playbook]
      end
   end
end
