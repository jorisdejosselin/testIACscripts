# Saltstack advanced administration test env

$bootstrap_master = <<-SCRIPT
cd ~ && curl https://raw.githubusercontent.com/saltstack/salt-bootstrap/stable/bootstrap-salt.sh -o bootstrap-salt.sh && sudo sh ./bootstrap-salt.sh -M -A 192.168.0.100
SCRIPT

$bootstrap_minion_debian = <<-SCRIPT
sudo apt install curl -y
cd ~ && curl https://raw.githubusercontent.com/saltstack/salt-bootstrap/stable/bootstrap-salt.sh -o bootstrap-salt.sh && sudo sh ./bootstrap-salt.sh -A 192.168.0.100
SCRIPT

$bootstrap_minion_centos = <<-SCRIPT
cd ~ && curl https://raw.githubusercontent.com/saltstack/salt-bootstrap/stable/bootstrap-salt.sh -o bootstrap-salt.sh && sudo sh ./bootstrap-salt.sh -A 192.168.0.100
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.define "gru" do |gru|
    gru.vm.box = "centos/7"
    gru.vm.hostname = "gru"
    gru.vm.network :private_network, ip: "192.168.0.100"
    gru.vm.provision :shell, inline: $bootstrap_master, run: 'always'

    gru.vm.provider :virtualbox do |vb|
      vb.customize [
        "modifyvm", :id,
        "--cpuexecutioncap", "100",
        "--memory", "1024",
      ]
    end
  end
  config.vm.define "jerry" do |jerry|
      jerry.vm.box = "centos/7"
      jerry.vm.hostname = "jerry"
      jerry.vm.network :private_network, ip: "192.168.0.101"
      jerry.vm.provision :shell, inline: $bootstrap_minion_centos, run: 'always'

      jerry.vm.provider :virtualbox do |vb|
        vb.customize [
          "modifyvm", :id,
          "--cpuexecutioncap", "100",
          "--memory", "1024",
        ]
    end
  end
  config.vm.define "stuart" do |stuart|
      stuart.vm.box = "centos/7"
      stuart.vm.hostname = "stuart"
      stuart.vm.network :private_network, ip: "192.168.0.102"
      stuart.vm.provision :shell, inline: $bootstrap_minion_centos, run: 'always'

      stuart.vm.provider :virtualbox do |vb|
        vb.customize [
          "modifyvm", :id,
          "--cpuexecutioncap", "100",
          "--memory", "1024",
        ]
    end
  end
  config.vm.define "kevin" do |kevin|
      kevin.vm.box = "debian/jessie64"
      kevin.vm.hostname = "kevin"
      kevin.vm.network :private_network, ip: "192.168.0.103"
      kevin.vm.provision :shell, inline: $bootstrap_minion_debian, run: 'always'

      kevin.vm.provider :virtualbox do |vb|
        vb.customize [
          "modifyvm", :id,
          "--cpuexecutioncap", "100",
          "--memory", "1024",
        ]
    end
  end
end
