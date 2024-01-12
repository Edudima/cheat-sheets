# Deshabilitar Swap Ubuntu 22.04

Como deshabilitar la memoria swap en una VM con Ubuntu.

#### 1. Comprobar si swap se encuentra habilitado y que cantidad de memoria tiene asignada

`swapon --show`

#### 2. Desactivar swap

`swapoff -a`

#### 3. Eliminar espacio asignado para swap editando el archivo fstab

`vi /etc/fstab`



    # /etc/fstab: static file system information.
    #
    # Use 'blkid' to print the universally unique identifier for a
    # device; this may be used with UUID= as a more robust way to name devices
    # that works even if disks are added and removed. See fstab(5).
    #
    # <file system> <mount point>   <type>  <options>       <dump>  <pass>
    # / was on /dev/ubuntu-vg/ubuntu-lv during curtin installation
    /dev/disk/by-id/dm-uuid-LVM-lkKyT23uUv21APU19iWs5lccmdaoi2CFrwRbre43cvKEIpzM4hxsYbD52IV1HGce / ext4 defaults 0 1
    # /boot was on /dev/sda2 during curtin installation
    /dev/disk/by-uuid/b18afecc-33c2-43de-b052-74e9891040a7 /boot ext4 defaults 0 1
    # /boot/efi was on /dev/sda1 during curtin installation
    /dev/disk/by-uuid/6D95-8678 /boot/efi vfat defaults 0 1
    #/swap.img       none    swap    sw      0       0

Comentamos la línea que se refiere a swap (en este caso, la última línea)

#### 4. Comprobación

Reiniciamos la VM, y ejecutamos el siguiente comando:

`free -h`

El resultado debería ser 0.
