# -*- mode: ruby -*-
# vi: set ft=ruby :

# NOTE: override this via the option --provider {provider_name}
ENV["VAGRANT_DEFAULT_PROVIDER"] = "parallels"

Vagrant.configure(2) do |config|
  config.vm.provider "parallels" do |vm|
    vm.linked_clone = true
    vm.update_guest_tools = true
  end

  # NOTE: test boxes obtained from https://atlas.hashicorp.com/boxcutter
  # packer build source repo: https://github.com/boxcutter
  operating_systems = %w{ ubuntu1404 }

  operating_systems.each do |os|
    config.vm.define os do |system|
      # osx built from boxcutter repo since the box is not publicly available
      if os =~ /^osx/ then
        system.vm.box = os
      else
        system.vm.box = "boxcutter/#{os}"
      end

      config.vm.provision "ansible" do |ansible|
        ansible.playbook = "deploy.yml"
        ansible.sudo = true
      end
    end
  end

end
