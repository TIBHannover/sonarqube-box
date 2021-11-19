require 'yaml'
settings = YAML.load_file 'ansible/group_vars/all.yml'

Vagrant.configure("2") do |config|

  config.vm.define "sonarqube-vm" do |srv|
    srv.vm.box = "debian/buster64"
    srv.ssh.insert_key = false
    srv.vm.hostname = "sonarqube.box"
    srv.vm.network :private_network, ip: settings['sonarqube_host']

    srv.vm.provider :virtualbox do |vb|
      vb.name = "sonarqube"
      vb.memory = 4096
      vb.cpus = 2
    end
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.install = true
    #ansible.install_mode = "pip"
    #ansible.pip_install_cmd = "sudo apt-get install -y python3-distutils && curl -s https://bootstrap.pypa.io/get-pip.py | sudo python3"
    ansible.version = "latest"
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "ansible/playbook.yml"
    ansible.galaxy_role_file = "requirements.yml"
    ansible.verbose = "true"
    ansible.groups = {
      "sonarqube" => ["sonarqube-vm"],
      "all:vars" => {
        "timezone" => "Europe/Berlin"
      }
    }
    ansible.host_vars = {
      "sonarqube-vm" => {
      }
    }
  end
end
