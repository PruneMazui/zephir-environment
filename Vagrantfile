VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "bento/centos-6.8"
  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip:"127.0.0.1"
  config.vm.synced_folder ".", "/source/"
  Encoding.default_external = 'UTF-8'

  config.vm.provider :virtualbox do |vb|
    # vb.gui = true
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.provision :shell, inline: <<-SHELL
    yum install -y epel-release
    rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
    yum install -y --enablerepo=remi,remi-php71 php php-devel
    yum install -y gcc make re2c autoconf git
    
    cd /usr/local/src
    git clone https://github.com/phalcon/zephir
    cd zephir
    ./install -c
SHELL

end
