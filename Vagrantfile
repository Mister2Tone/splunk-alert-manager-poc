# -*- mode: ruby -*-
# vi: set ft=ruby :

servers=[
	{
	 :hostname => "master-splunk",
	 :ip => "192.168.56.5",
	 :box => "badarsebard/centos-7.5-splunk",
	 :ram => 1024,
	 :cpu => 1
	},
	{
	 :hostname => "sh-splunk",
	 :ip => "192.168.56.15",
	 :box => "badarsebard/centos-7.5-splunk",
	 :ram => 1024,
	 :cpu => 1
	},
	{
	  :hostname => "idx-splunk",
          :ip => "192.168.56.25",
          :box => "badarsebard/centos-7.5-splunk",
          :ram => 1024,
          :cpu => 1
	}
]

Vagrant.configure("2") do |config|
	
	config.vm.box_check_update = false
	config.vm.synced_folder ".","/vagrant", disabled:true

	servers.each do |machine|

		config.vm.define machine[:hostname] do |node|
		
		   node.vm.box = machine[:box]
		   node.vm.hostname = machine[:hostname]
		   node.vm.network "private_network", ip: machine[:ip]

		   node.vm.provider "virtualbox" do |vb|
		      vb.customize ["modifyvm", :id, "--memory", machine[:ram], "--cpus", machine[:cpu]]
		      vb.name = machine[:hostname]
		   end

	           config.ssh.insert_key = false
	           config.ssh.private_key_path = ["~/.vagrant.d/insecure_private_key","~/.ssh/id_rsa"]

		end

	end
	
	config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"	

 	config.vm.provision "ansible" do |ansible|
 	   #ansible.limit = "all"
 	   ansible.playbook = "playbook.yml"
 	   #ansible.inventory_path = "ansible_inventory"
 	   #ansible.host_key_checking = false
 	   #ansible.verbose = "v"
 	end

end
