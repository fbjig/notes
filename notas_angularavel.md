# Angular - Laravel
    sudo apt install nodejs
    sudo apt install npm
    sudo npm install -g typescript  # si falla => npm config set strict-ssl false
    sudo npm install -g @angular/cli
  
  Si se usa sudo y dice que no tiene permiso y saltan errores, añadir esto a los comandos:
    
    --unsafe-perm=true
    
Nuevo proyecto:

    sudo ng new nombreCarpeta --unsafe-perm=true

Acceso desde remoto:

    ng serve --host 0.0.0.0
    
