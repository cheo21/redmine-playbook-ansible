Vagrant.configure("2") do |config|
  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/jammy64"
    ubuntu.vm.hostname = "ubuntu-test"

    config.vm.network "forwarded_port",
    guest: 3000, host: 8888, host_ip: "127.0.0.1"

    ubuntu.vm.provision "ansible" do |ansible|
      install_mode = :default
      ansible.playbook = "playbook.yml"
    end
  end
end