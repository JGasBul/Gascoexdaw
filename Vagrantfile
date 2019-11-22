# Examen Pepe Gascó Bule.
# Lo que hace es que se creen en una carpeta llamada shared_Directory dos carpetas llamadas www y sites-available.
# Gracias a esto, en la maquina solo se tendria que modificar el archivo /etc/hosts. El resto se puede hacer tranquilamente en nuestro windows ya que las carpetas estan vinculadas con la maquina.

Vagrant.configure("2") do |config|

  config.vm.box = "hashicorp/precise32"
  config.vm.hostname = "ExamenPepeGascoBule"

  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "private_network", ip: "192.168.1.116"
  config.vm.synced_folder "../shared_Directory", "/shared_Directory"

  config.vm.provision "shell", inline: <<-SHELL
    apt-get -y update
    apt-get install -y apache2
    apt-get install -y elinks
    mkdir /shared_Directory/apache
    mkdir /shared_Directory/apache/www 
    cp /var/www/index.html /shared_Directory/apache/www/ 
    sudo rm -r /var/www/ 
    sudo ln -s /shared_Directory/apache/www/ /var/ 
    cp -r /etc/apache2/sites-available/ /shared_Directory/apache/
    sudo rm -r /etc/apache2/sites-available/
    sudo ln -s /shared_Directory/apache/sites-available/ /etc/apache2/
  SHELL
end
