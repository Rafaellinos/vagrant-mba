$script_inline = <<-SCRIPT
  debconf-set-selections <<< 'mysql-server mysql-server/root_password password root' && \
  debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root' && \
  apt-get update && apt-get install -y mysql-server-5.7 && \
  sed -i "s/.*bind-address.*/bind-address = 0.0.0.0/" /etc/mysql/mysql.conf.d/mysqld.cnf && \
  mysql -u root -proot -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION; FLUSH PRIVILEGES; SET GLOBAL max_connect_errors=10000;" && \
  sudo service mysql restart
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = 2048
    vb.cpus = 2
  end

  config.vm.define "mysqlserver" do |mysqlserver|
    mysqlserver.vm.network "forwarded_port", guest: 3306, host: 3339
    mysqlserver.vm.provider "virtualbox" do |vb|
      vb.name = "mysqlserver"
    end
    
    mysqlserver.vm.provision "shell", privileged: true, inline: $script_inline

  end

end