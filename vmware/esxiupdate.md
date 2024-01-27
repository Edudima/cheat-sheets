# Actualización ESXi vía CLI

Como actualizar nuestros hosts ESXi vía CLI mediante repositorio online u offline

#### 1. Habilitar SSH en nuestro host

Accedemos a nuestro ESXi y nos dirigimos a:

Host > Administrar > Servicios 

![](https://www.edudima.com/wp-content/uploads/2024/01/esxissh.png)

Y hacemos click en "Iniciar"

#### 2. Habilitar modo mantenmiento en el host	

Pondremos el host en modo mantenmiento. Las VMs que se encuentren funcionando sobre ese host, han de ser movidas o apagadas previamente.

Lo podemos realizar desde la interfaz web, o desde el acceso SSH con el siguiente comando:

`esxcli system maintenanceMode set –enable true`

#### 3. Habilitamos http y https en el firewall de nuestro ESXi

Para poder realizar la descarga con garantías, introducimos este comando:

`esxcli network firewall ruleset set -e true -r httpClient`

#### 4. Comprobamos las versiones disponibles online

Con el siguiente comando, revisaremos el catálogo de versiones disponibles para descargar. Encontraremos las versiones "standard", "no-tools" (por si queremos encargarnos nosotros de administrar el repositorio de VMware Tools), o "s" (security patches)

`esxcli software sources profile list --depot=https://hostupdate.vmware.com/software/VUM/PRODUCTION/main/vmw-depot-index.xml`

Si queremos filtrar por una versión de ESXi concreta (ej. 7), introduciremos dicho filtro en el comando:

`esxcli software sources profile list --depot=https://hostupdate.vmware.com/software/VUM/PRODUCTION/main/vmw-depot-index.xml | grep -i ESXi-7`

#### 5. Lanzamos la actualización

Una vez localizada la versión a la que queremos actualizar, introduciremos el siguiente comando (aquí va con un ejemplo de 7.0U3o)

`esxcli software profile update -p ESXi-7.0U3o-22348816-standard -d https://hostupdate.vmware.com/software/VUM/PRODUCTION/main/vmw-depot-index.xml`

#### 6. Actualización Offline

Para realizar esta operación, descargaríamos de la página oficial de VMware el archivo .zip correspondiente a la versión que quisiéramos descargar, y lo subiríamos a un repositorio al cual nuestro ESXi tuviese acceso.

Una vez subido, podríamos verificar las versiones disponibles en ese .zip que hemos descargado con el siguiente comando:

`esxcli software sources profile list -d /vmfs/volumes//xxxxxxxx-xxxxxxxx-xxxx-xxxxxxxxxxxx/VMware-ESXi-7.0U3o-22348816-depot.zip`

En lugar de las "xxxxx", habría que introducir el path de nuestro repositorio. 
En el output, veríamos en este caso las versiones "standard" y "no-tools" de la versión que indico en el ejemplo (ESXi-7.0U3o). 

Solo nos quedaría introducir el comando de actualización:

`esxcli software profile update -p ESXi-7.0U3o-22348816-standard -d /vmfs/volumes//xxxxxxxx-xxxxxxxx-xxxx-xxxxxxxxxxxx/VMware-ESXi-7.0U3o-22348816-depot.zip`

#### 7. Comprobación

Tras realizar el update, sea cual sea el método, recibiremos un output de nuestro ESXi, indicando los paquetes modificados y no modificados, posibles errores, y si es necesario realizar un reinicio del mismo.

Una vez reiniciado, volvemos a dejar el firewall como estaba:

`esxcli network firewall ruleset set -e false -r httpClient`

Y sacamos nuestro host de modo mantenimiento:

`esxcli system maintenanceMode set –enable false`

Ya solo quedaría volver a mover / encender máquinas y comprobar que todo funciona correctamente.
