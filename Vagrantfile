$script_mysql = <<-SCRIPT
    apt-get update && \
    apt-get install -y mysql-server-5.7 && \
    mysql -e "create user 'admin'@'%' identified by 'pass';"
SCRIPT
Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/bionic64"
    config.vm.network "forwarded_port", guest: 3306, host: 3306
    config.vm.network "public_network"
    config.vm.provision "shell", inline: $script_mysql
    config.vm.provision "shell", inline: "sed -i -e 's/127.0.0.1/0.0.0.0/g' /etc/mysql/mysql.conf.d/mysqld.cnf"
    config.vm.provision "shell", inline: "service mysql restart"
end
