# Pasos seguidos para crear un sistema de backup online usando el BitTorrent y una Cubietruck (Cubieboard 3)

## Consideraciones iniciales sobre el documento

En este documento se detallan los pasos seguidos para instalar el Lubuntu en una Cubietruck (Cubieboard 3) y el BitTorrent Sync.  
Los pasos detallados son los que yo he seguido y que a mí me han funcionado.  
En mi caso en la tarjeta SD está el sistema operativo y las aplicaciones, en el disco duro sólo se encuentran los ficheros del BitTorrent Sync.

## Instalación del sistema operativo en tarjeta SD
En este apartado se detallan los pasos para realizar la instalación del Lubuntu dentro de la tarjeta SD.

### Consideraciones iniciales
Para realizar los pasos detallados a continuación se ha utilizado un sistema Ubuntu.  
La tarjeta SD estaba montada como `sdb`.

### Instalación del sistema operativo dentro de la tarjeta SD
El sistema operativo sobre el que se han realizado las acciones siguientes ha sido el Lubuntu para la cubieboard, aunque la versión de linux sobre la que se ejecuten no debería de importar.

Los pasos seguidos han sido los siguientes:

* Asignación de la ruta en la que está la tarjeta a una variable del sistema
``` bash
card=/dev/sdb
```

* Limpieza de la tarjeta SD:
``` bash
sudo dd if=/dev/zero of=${card} bs=1024 seek=544 count=128
```

* Hacer la tarjeta SD arrancable:
``` bash
sudo dd if=u-boot-sunxi-with-spl-ct-20131102.bin of=$card bs=1024 seek=8
```

* Particionado de la tarjeta SD: Esta se ha de particionar en 2 particiones, la primera de 64Mb. (2048 sectores) y la segunda del resto del tamaño. Ejemplo de como se queda:
``` bash
 Device Boot      Start         End      Blocks   Id  System
/dev/sdb1            2048      133119       65536   83  Linux
/dev/sdb2          133120    15278079     7572480   83  Linux
```
Para poder realizar la modificación de la partición se ha usado el comando siguiente:
``` bash
sudo fdisk $card
```

* Formateado de las particiones creadas:
``` bash
sudo mkfs.ext2 ${card}1
sudo mkfs.ext4 ${card}2
```

* Copiado de los datos a la tarjeta SD:
``` bash
mkdir /tmp/sdb1 /tmp/sdb2
sudo mount -t ext2 ${card}1 /tmp/sdb1
sudo mount -t ext4 ${card}2 /tmp/sdb2
sudo tar -C /tmp/sdb1 -xvf bootfs-part1.tar.gz
sudo tar -C /tmp/sdb2 -xvf rootfs-part2.tar.gz
sync
sudo umount /tmp/sdb1
sudo umount /tmp/sdb2
```

### Configuración del sistema operativo

#### Configuración del teclado en español:

Para esto ejecutamos el siguiente comando:

``` bash
sudo dpkg-reconfigure keyboard-configuration
```
Este comando se encarga de lanzar la aplicación de reconfiguración del teclado.
Seleccionamos **Generic 105 key (Intl PC)**, el idioma **Spanish** y luego las opciones predeterminadas con **OK**.

#### Configuración de red:

En mi caso no la he tocado, ya que uso el DHCP, que es la configuración que viene por defecto.

#### Configuración de la zona horaria:

Para esto ejecutamos el siguiente comando:

``` bash
sudo dpkg-reconfigure tzdata
```
Este comando se encarga de lanzar la aplicación de reconfiguración de la zona horaria.
Seleccionamos la zona geográfica **Europe** y la zona horaria **Madrid**.

#### Cambio del nombre a la cubieboard:

Para esto tenemos que crear/modificar el fichero **/etc/hosts** y añadir el nombre que deseemos que tenga la cubieboard.

Para ello ejecutaremos el siguiente comando:

``` bash
sudo nano/etc/hosts
```

Y añadiremos la siguiente línea, donde *cubieboard* es el nombre que le asignaremos:

```
127.0.0.1 cubieboard
```

#### Montado del disco duro:

En mi caso el disco duro es **/dev/sda1**.  
El disco duro se va a montar sobre la carpeta **/media/hdd**.  
Para montar el disco duro y que la configuración se guarde entre arranques del sistema operativo se ha de modificar el fichero **/etc/fstab**. Para ello añadiremos la siguiente línea a dicho fichero.

```
/dev/sda1 /media/hdd ext4 defaults 0 2
```

# Instalación y configuración del Bitorrent Sync

## Consideraciones iniciales

Las consideraciones inciales son las siguientes:

* El BitTorrent Sync lo descargo dentro de la carpeta **/home/linaro/Downloads/** y se descomprime dentro de **/home/linaro/Downloads/btsync**.
* El binario lo dejo dentro de la carpeta **/usr/local/bin/**.
* La configuración del programa está en el fichero **/etc/btsync/btsync.conf**.
* Tengo un script de arranque del programa, para que este arranque al arrancar el sistema operativo.
* El disco duro se ha montado sobre la carpeta: **/media/hdd/**.

## Proceso de instalación

* Descarga del Bittorrent Sync.
``` bash
wget http://download-new.utorrent.com/endpoint/btsync/os/linux-arm/track/stable
mkdir btsync
mv stable btsync_arm.tar.gz
tar zxvf btsync_arm.tar.gz -C btsync
```

* Creamos variables del sistema para ayudarnos en la creación
``` bash
config="/etc/btsync/btsync.conf"
user="root"
```

* Comando a ejecutar para que el programa arranque, en mi caso ha hecho falta, aunque no siempre es preciso. Este paso consiste en linkar el nombre de una librería, para que el programa pueda encontrarla. Esto es necesario para cuando se lance el comando del punto siguiente y este de un error.
``` bash
ln -s /lib/arm-linux-gnueabihf/ld-linux.so.3 /lib/ld-linux.so.3
```

* Extracción del fichero de configuración por defecto.
btsync --dump-sample-config > $config

* Reconfiguración del fichero de configuración por defecto. Para ello se lanzan los siguientes comandos.
``` bash
sed -i 's/"device_name"\s*:\s*"My Sync Device"/"device_name": "CUBIEBOARD"/g' $config
sed -i 's/"storage_path"\s*:\s*"\/home\/user\/\.sync"/"storage_path": "\/media\/hdd\/btsync"/g' $config
sed -i 's/"login"\s*:\s*"admin",//g' $config
sed -i 's/"password"\s*:\s*"password"//g' $config
sed -i 's/:8888",/:8888"/g' $config
```
Como puede observarse se han cambiado los parámetros *device_name*, *storage_path*, *login* y *password*. Los comandos anteriores tambien pueden cambiarse por un simple `nano $config` y cambiar los parámetros de forma manual. De todas formas es recomandable lanzar este último parámetro para revisar la configuración y ver si se quiere cambiar algún parámetro más.

* Creación del script de arranque automático.
``` bash
mkdir /var/run/btsync/
nano /etc/init.d/btsync
```

El contenido del fichero `/etc/init.d/btsync` es el siguiente:

``` bash
#! /bin/sh
### BEGIN INIT INFO
# Provides: btsync
# Required-Start: \$syslog \$remote_fs
# Required-Stop: \$syslog \$remote_fs
# Should-Start: \$local_fs
# Should-Stop: \$local_fs
# Default-Start: 2 3 4 5
# Default-Stop: 0 1 6
# Short-Description: btsync - Bittorent SyncApp
# Description: btsync - Bittorent SyncApp
### END INIT INFO

user=root
group=root

# the full path to the filename where you store your rtorrent configuration
config="/etc/btsync/btsync.conf"

# set of options to run with
options=""

PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
DAEMON=/usr/local/bin/btsync
DAEMON_ARGS="--config \$config"
NAME=btsync
DESC=btsync

RUNDIR=/var/run/syncapp
PIDFILE=/var/run/btsync.pid

test -x \$DAEMON || exit 0

if [ -r /etc/default/\$NAME ]
then
. /etc/default/\$NAME
fi

set -e

case "\$1" in
    start)
    echo -n "Starting \$DESC: "
    mkdir -p \$RUNDIR
    touch \$PIDFILE
    chown \$user:\$group \$RUNDIR \$PIDFILE
    chmod 755 \$RUNDIR

    if [ -n "\$ULIMIT" ]
    then
    ulimit -n \$ULIMIT
    fi

    if start-stop-daemon --start --quiet --umask 007 --pidfile \$PIDFILE --chuid \$user:\$group --exec \$DAEMON -- \$DAEMON_ARGS
    then
    echo "\$NAME."
    else
    echo "failed"
    fi
    ;;

    stop)
    echo -n "Stopping \$DESC: "
    killall -w btsync || true
    sleep 1
    rm -f \$PIDFILE || true
    ;;

    status)
    echo -n "\$DESC is "
    if start-stop-daemon --stop --quiet --signal 0 --name \${NAME} --pidfile \${PIDFILE}
    then
    echo "running"
    else
    echo "not running"
    exit 1
    fi
    ;;

    *)
    echo "Usage: /etc/init.d/\$NAME {start|stop|status}" >&2
    exit 1
    ;;
esac

exit 0
```

* Arranque del programa
``` bash
chmod +x /etc/init.d/btsync
update-rc.d btsync defaults
```

## Actualización del Bittorrent Sync

Para actualiar el programa me he creado el siguiente script, este se encuentra dentro de **/home/linaro/Downloads/**. El mismo script se encarga de descargar, extraer, mover el ejecutable y reiniciar el servicio.  
El script es el siguiente:

``` bash
#!/bin/bash

rm -Rf btsync
mkdir btsync

wget http://download-new.utorrent.com/endpoint/btsync/os/linux-arm/track/stable

mv stable btsync_arm.tar.gz
tar zxvf btsync_arm.tar.gz -C btsync

service btsync stop

cp ./btsync/btsync /usr/local/bin/

service btsync start
```

# Información obtenida de:

[Instalación del linux en la SD](http://docs.cubieboard.org/tutorials/ct1/installation/install_lubuntu_desktop_server_to_sd_card)

[Configuración del linux](https://www.imai-solutions.com/cubieboard-lubuntu)

[Configuración del bittorrent sync](http://quadfinity.blogspot.com.es/2013/11/Install-BitTorrent-Sync-on-Cubieboard-A10.html)

[Fstab](https://help.ubuntu.com/community/Fstab)

