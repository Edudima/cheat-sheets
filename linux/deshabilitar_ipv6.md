# Deshabilitar IPv6 Ubuntu 22.04 permanentemente

Como deshabilitar IP v6 permanentemente en una VM con Ubuntu.

#### 1. Editar el archivo sysctl.conf

`vi /etc/sysctl.conf`

#### 2. Añadir las siguientes líneas al final del archivo

    net.ipv6.conf.all.disable_ipv6=1
    net.ipv6.conf.default.disable_ipv6=1
    net.ipv6.conf.lo.disable_ipv6 = 1

#### 3. Aplicar los cambios realizados

`sysctl -p`

#### 4. Comprobar que IPv6 se encuentre desactivado

`cat /proc/sys/net/ipv6/conf/all/disable_ipv6`

Si recibimos un output "1", habremos desactivado IPv6 en nuestra máquina.
