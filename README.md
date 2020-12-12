# vagrant-mba

# Acesso ao mysql da vm
mysql --host=127.0.0.1 --port=3306 -u root -proot


# Commandos
vagrant up # iniciar box
vagrant ssh # acesso ssh
vagrant status # verificar status
vagrant halt # desligar
vagrant reload # equivalente a halt && up
vagrant destroy -f # destriuir vm
vagrant box list # listar "imagens"
vagrant reload --provision
