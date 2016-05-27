def configure_vm(vm, **opts)

	vm.box = opts.fetch(:box, "centos/7")
		
    vm.network :private_network, ip: opts[:private_ip]

    vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end
    
    vm.provider :libvirt do |domain|
		domain.memory = opts.fetch(:memory, 4096)
		domain.cpus = opts.fetch(:cpus, 2)
		domain.nested = true
	end

	# Disable default share, because we dont use it
	vm.synced_folder ".", "/vagrant", disabled: true
end


def apply_ansible(vm, playbook)
	vm.provision :ansible do |ansible|
		ansible.host_key_checking = false
		ansible.playbook = playbook
		ansible.verbose = "v"
	end
end


Vagrant.configure(2) do |config|



	# ---------------------------------------------------------------------------------------------
	#
	# Definition of the VM for running kubernetes master.
	#
	config.vm.define "master" do |master|
	
		configure_vm(master.vm, private_ip: "192.168.123.110")

		apply_ansible(master.vm, "ansible-master.yaml")

	end


	# ---------------------------------------------------------------------------------------------
	#
	# Definition of the VM for running kubernetes node.
	#
	config.vm.define "node" do |node|
	

		configure_vm(node.vm, private_ip: "192.168.123.120")

		apply_ansible(node.vm, "ansible-node.yaml")

	end


end
