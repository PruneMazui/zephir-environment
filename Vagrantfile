VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos/7"
  config.vm.network :private_network, ip: "10.10.10.10"
  config.vm.synced_folder ".", "/source/"
  Encoding.default_external = 'UTF-8'

  config.vm.provider :virtualbox do |vb|
    # vb.gui = true
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.provision :shell, inline: <<-SHELL
    yum install -y epel-release
    yum install -y http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
    yum install -y --enablerepo=remi-php71 php php-devel php-xml php-pecl-zip php-pdo php-mbstring php-pecl-xdebug
    yum install -y gcc-c++ make automake re2c autoconf git unzip
    
    cd /usr/local/src
    git clone git://github.com/phalcon/php-zephir-parser.git
    cd php-zephir-parser/
    ./install

    cat <<EOT > /etc/php.ini
[Zephir Parser]
extension=zephir_parser.so
EOT
    
    cd /usr/local/src
    git clone https://github.com/phalcon/zephir
    cd zephir
    ./install -c
SHELL

end
