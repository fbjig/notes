# Configuración de entorno de desarrollo

## Máquina virtual de Ubuntu Server

Primero instalamos Ubuntu Server (montando una ISO) en el VirtualBox. Previa instalación ponemos Adaptador en Puente para nuestra red inalámbrica.

Luego, una vez instalado Ubuntu, configuramos la red. Probamos a hacer un ping a "google.es", y si da error, hacemos lo siguiente:

    sudo nano /etc/network/interfaces
  
Y ponemos lo siguiente (eliminando lo anterior):
  
    iface eth0 inet static
    address 192.168.1.151   # la ip que queramos poner
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
  
Luego reiniciamos el servicio de red y probamos ping de nuevo.

    sudo ifdown eth0
    sudo ifup eth0
    ping google.es
  
## Configuración SSH para manejar la máquina virtual por Putty

Instalamos SSH.

    sudo apt update
    sudo apt install ssh
    
Cargamos Putty y ponemos la IP que hemos indicado en address (paso anterior).

## Configuración Samba (ver archivos desde windows)

Instalamos samba:
    
    sudo apt-get install samba samba-common python-glade2 system-config-samba

Configuramos samba:
    
    sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.backup
    sudo nano /etc/samba/smb.conf
    
Ponemos lo siguiente en el archivo de configuración:

    [fernando]
    comment = Directorio de samba
    path = /var/www
    browseable = yes
    writeable = yes
    public = yes
    create mask = 0755
    directory mask = 0755
    
Ponemos contraseña al usuario con el que se accedera desde windows:

    sudo smbpasswd -L -a fernando

Reiniciamos samba:

    sudo /etc/init.d/smbd restart

## Instalación de Apache, PHP y MySQL

    sudo apt-get update
    sudo apt-get upgrade
    
    sudo apt-get install apache2
    
    sudo apt-get install mysql-server
    
    sudo apt-get install php libapache2-mod-php php-mcrypt php-mysql php-cgi php-curl php-json
    
Si por lo que sea no se puede instalar el PHP (7.1 o mayor en fecha 2018-11) porque tenemos un Ubuntu viejo, instalar los repositios ondrej y ejecutar la misma orden conla version de php especificada.

    sudo add-apt-repository ppa:ondrej/php
    sudo apt-get update
    sudo apt-get install php7.1 libapache2-mod-php7.1 php7.1-mcrypt php7.1-mysql php7.1-cgi php7.1-curl php7.1-json
    
