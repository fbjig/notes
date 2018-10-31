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
  
 
