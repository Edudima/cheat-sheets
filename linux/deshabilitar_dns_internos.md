# Deshabilitar resolución interna DNS Ubuntu 22.04

Como deshabilitar la resolución de DNS interna en máquinas con Ubuntu 22.04 y posteriores.

Sin la realización de estos pasos, aunque realicemos una configuración IP correcta marcando los diferentes servidores DNS y dominios de búsqueda, la resolución DNS puede no funcionar correctamente.

#### 1. Detener y deshabilitar systemd-resolved

    sudo systemctl stop systemd-resolved
    sudo systemctl disable systemd-resolved

#### 2. Eliminar el link al archivo resolv.conf

Sin este paso, no podremos modificar posteriormente dicho archivo.

`sudo unlink /etc/resolv.conf`

#### 3. Editar el archivo resolv.conf

`vi /etc/resolv.conf`

El archivo se encontrará en blanco. Simplemente añadiremos nuestros DNS con la siguiente estructura:

    nameserver xxx.xxx.xxx.xxx
    nameserver xxx.xxx.xxx.xxx
    nameserver xxx.xxx.xxx.xxx
