# Recreacion del sistema de backup online usando el Resilio Sync y una Cubietruck (Cubieboard 3)

## Finalidad del artículo

La finalidad inicial del artículo ha sido la de cómo actualizar el linux de la Cubietruck y después migrar de Bittorrent Sync a Resilio Sync, pero por descuido no he creado una copia de seguridad de la tarjeta y actualizando el linux éste ha dejado de funcionar. Por tanto el artículo he tenido que cambiarlo de una actualización y migración a una creación total de la máquina desde cero, pero en este caso he añadido, además del Resilio Sync, el monitor creado con AngularJs y NodeJs para controlar la máquina.

Por si a alguien le interesa y desea intentar actualizar el linux indico a continuación los pasos que he seguido, hasta que me ha fallado, pero le recomiendo encarecidamente que haga una copia de seguridad de la tarjeta por si acaso le pasa lo mismo que a mí.

### Actualización del linux:

Antes que nada indicar que hace tiempo pude hacer una actualización del sistema operativo y ejecuté los siguientes pasos:

* Primero actualicé las librerías a su última versión.

``` bash
sudo apt-get update
sudo apt-get upgrade
```

* Depués actualicé el gestor de paquetes **apt**.

``` bash
apt-get check
apt-get install apt
```

* Por último subí la versión del linux.

``` bash
do-release-upgrade

apt update
apt dist-upgrade
```

Esta última vez he seguido los siguientes pasos.

* Primero he actualizado las librerías a su última versión:

``` bash
sudo apt-get update
sudo apt-get upgrade
```

* Después he subido la versión del linux.

``` bash
do-release-upgrade
```

La ejecución del anterior paso me ha dado como resultado el siguiente error: `The required dependency 'apt (>= 1.0.1ubuntu2.13)' is not installed.`.  
Para solucionarlo he bajado el paquete deb que pide desde la siguiente url: [https://launchpad.net/ubuntu/trusty/armhf/apt/1.0.1ubuntu2.13](https://launchpad.net/ubuntu/trusty/armhf/apt/1.0.1ubuntu2.13).

``` bash
wget http://launchpadlibrarian.net/254525360/apt_1.0.1ubuntu2.13_armhf.deb
```

Una vez descargado el fichero lo he instalado ejecutando el siguiente comando.

``` bash
dpkg -i apt_1.0.1ubuntu2.13_armhf.deb
```

* He vuelto a ejecutar el comando de actualización:

``` bash
do-release-upgrade
```

He vuelto a obtener otro error, en este caso ha sido el siguiente: `Error: The required dependency 'dpkg (>= 1.17.5ubuntu5.6)' is not installed`.  
Para solucionarlo he bajado el paquete deb que pide desde la siguiente url: [https://launchpad.net/~ubuntu-security/+archive/ubuntu/ppa/+build/9631646](https://launchpad.net/~ubuntu-security/+archive/ubuntu/ppa/+build/9631646)

``` bash
wget https://launchpad.net/~ubuntu-security/+archive/ubuntu/ppa/+build/9631646/+files/dpkg_1.17.5ubuntu5.6_armhf.deb
```

Una vez descargado el fichero lo he instalado ejecutando el siguiente comando.

``` bash
dpkg -i dpkg_1.17.5ubuntu5.6_armhf.deb
```

* He vuelto a ejecutar el comando de actualización:

``` bash
do-release-upgrade
```

Si después de ejecutar el comando anterior y reiniciar la máquina, esta arranca (en mi caso no lo ha hecho), se han de ejecutar los siguientes comandos para actualizar las librerías a la versión final.

``` bash
apt update
apt dist-upgrade
```

## Consideraciones iniciales sobre el artículo

En este artículo se detallan los pasos seguidos para instalar el Lubuntu Server en una Cubietruck (Cubieboard 3) y el Resilio Sync.  
Los pasos detallados son los que yo he seguido y que a mí me han funcionado.  
En mi caso en la tarjeta SD está el sistema operativo y las aplicaciones, en el disco duro sólo se encuentran los ficheros del BitTorrent Sync.  
He aprovechado para instalar el Linaro Server y no el Linaro, como tenía la máquina anterior, de esta forma he conseguido que ocupe menos en la tarjeta sd.

## Instalación del sistema operativo en la SD

Desde su [página oficial](http://cubieboard.org) y partir de esta ruta [Home › Model › cubieboard3(cubietruck)](http://cubieboard.org/model/cb3/) he descargado la siguiente imagen: [linaro-server-ct-card0-hdmi&vga-v1.0.img.7z](http://dl.cubieboard.org/model/CubieBoard3/Image/Linaro-server/linaro-server-ct-card0-hdmi&vga-v1.0.img.7z)

Después de descargarla la he grabado en la tarjeta SD.

##  Configuración del sistema operativo

Para la configuración del sistema operativo he seguido los siguientes pasos.

### Configuración del teclado en español:

Para esto ejecutamos el siguiente comando:

``` bash
sudo dpkg-reconfigure keyboard-configuration
```

Este comando se encarga de lanzar la aplicación de reconfiguración del teclado.
Seleccionamos **Generic 105 key (Intl PC)**, el idioma **Spanish** y luego las opciones predeterminadas con **OK**.

### Configuración de red:

En mi caso no la he tocado, ya que uso el DHCP, que es la configuración que viene por defecto.

### Configuración de la zona horaria:

Para esto ejecutamos el siguiente comando:

``` bash
sudo dpkg-reconfigure tzdata
```

Este comando se encarga de lanzar la aplicación de reconfiguración de la zona horaria.
Seleccionamos la zona geográfica **Europe** y la zona horaria **Madrid**.

### Cambio del nombre a la cubieboard:

Para esto tenemos que crear/modificar el fichero **/etc/hosts** y añadir el nombre que deseemos que tenga la cubieboard.
Para ello ejecutaremos el siguiente comando:

``` bash
sudo vi /etc/hosts
```

Y cambiaremos los nombres de la máquina en las siguientes líneas, quedando de la siguiente forma:

```
127.0.0.1       CUBIEBOARD
127.0.1.1       CUBIEBOARD
```

y el fichero **/etc/hostname**

``` bash
sudo vi /etc/hostname
```

Cambiando el nombre que allí se encuentra por el de la máquina:

```
CUBIEBOARD
```

###  Montado del disco duro:
En mi caso el disco duro es **/dev/sda1**.  
El disco duro se va a montar sobre la carpeta **/media/hdd**.  
Para montar el disco duro y que la configuración se guarde entre arranques del sistema operativo se ha de modificar el fichero **/etc/fstab**, usando el siguiente comando:

``` bash
sudo vi /etc/fstab
```

Para ello añadiremos la siguiente línea a dicho fichero.

```
/dev/sda1 /media/hdd ext4 defaults 0 2
```

### Actualización del sistema operativo

Para actualizar los paquetes del sistema operativo se han ejecutado los siguientes comandos:

``` bash
sudo apt-get update
sudo apt-get upgrade
```


## Instalación de Resilio Sync

Para instalar el programa desde **apt-get**, he seguido la información del siguiente enlace: https://www.resilio.com/blog/official-linux-packages-for-sync-now-available

### Preparación del repositorio

Para preparar el repositorio se crea el fichero **/etc/apt/sources.list.d/resilio-sync.list**, ejecutando el siguiente comando:

``` bash
sudo vi /etc/apt/sources.list.d/resilio-sync.list
```

Se añade la siguiente linea:

```
wget -qO - https://linux-packages.resilio.com/resilio-sync/key.asc | sudo apt-key add -
```

### Instalación

Para instalar la aplicación se ejecuta el siguiente comando.

``` bash
sudo apt-get update
sudo apt-get install resilio-sync
```

### Configuración

Para configurar el Resilio Sync y poder aprovechar lo que ya tenía del Bittorrent Sync he realizado los siguientes pasos:

* Nos movemos a la carpeta de configuración del Resilio Sync.

``` bash
cd /etc/resilio-sync
```

* Creamos variables del sistema para ayudarnos en este proceso:

``` bash
config="/etc/resilio-sync/config.json"
user="root"
```

* Extraemos el fichero de configuración por defecto del Resilio Sync:

``` bash
rslsync --dump-sample-config > $config
```


* Reconfiguramos el fichero de configuración por defecto. Para ello se lanzan los siguientes comandos.

``` bash
sed -i 's/"device_name"\s*:\s*"My Sync Device"/"device_name": "CUBIEBOARD"/g' $config
sed -i 's/"storage_path"\s*:\s*"\/home\/user\/\.sync"/"storage_path": "\/media\/hdd\/btsync"/g' $config
sed -i 's/"login"\s*:\s*"admin",//g' $config
sed -i 's/"password"\s*:\s*"password"//g' $config
sed -i 's/:8888",/:8888"/g' $config
```

* Después editamos el fichero de configuración por defecto

``` bash
vi /etc/resilio-sync/config.json
```

y descomentamos las líneas que contengan **device_name** y **storage_path** si estaban comentadas en el fichero.


### Uso datos anteriores de BitTorrnent Sync

Para que pueda tener acceso al disco duro anterior hay que cambiar que el usuario que arranca el servicio, en nuestro caso es root y no rslsync, para ello hay que modificar el fichero /etc/init.d/resilio-sync.

``` bash
vi /etc/init.d/resilio-sync
```

y cambiamos

```
SYNC_USER=rslsync
```

por

```
SYNC_USER=root
```

y además cambiamos

```
start-stop-daemon --start --quiet -b -o -c $SYNC_USER -u $SYNC_USER --exec $DAEMON --umask 0002 -- --config $CONFIG
```

por

```
start-stop-daemon --start --quiet -b -o -c $SYNC_USER -u $SYNC_USER --exec $DAEMON --umask 0007 -- --config $CONFIG
```


Después de esto ya podemos reiniciar la cubietruck.

``` bash
sudo shutdown -h 0
```

#### Información adicional

[Pasos seguidos para crear un sistema de backup online usando el BitTorrent y una Cubietruck (Cubieboard 3)](../2014/pasos_seguidos_para_crear_un_sistema_de_backup_online_usando_el_bittorrent_y_una_cubietruck_cubieboard_3.md)  
[Upgrade on dekstops (BitTorrent Sync -> Resilio Sync) ](https://help.getsync.com/hc/en-us/articles/211928186-Upgrade-on-dekstops-BitTorrent-Sync-Resilio-Sync-)  
[Official Linux Packages for Sync Now Available](https://www.resilio.com/blog/official-linux-packages-for-sync-now-available)  


## Instalación del monitor basado en AngularJs y NodeJs

Basándome en el siguiente artículo [Monitor basado en AngularJs y NodeJs para la Cubietruck (Cubieboard 3)](../2016/monitor_basado_en_angularjs_y_nodejs_para_la_cubietruck_cubieboard_3.md) he instalado el monitor.


###  Software instalado

#### Git

Este es el cliente usado para descargar la web desde github.
Para la instalación he ejecutado los siguientes comandos:

``` bash
sudo apt-get install git
```

#### NodeJS

Para la instalación de NodeJS he elegido la última versión (en el momento de escribir el artículo es la 6.x) y he ejecutado los siguientes comandos:

``` bash
sudo apt-get install curl
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```

##### Información adicional

[Installing Node.js via package manager](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions)

###  Librerías adicionales que he instalado en la Cubieboard para poder realizar la monitorización

#### lm-sensors

Para poder detectar la temperatura de la CPU he usado la herramienta lm-sensors.
Los pasos que he seguido para instalarla han sido los siguientes:

Primero he ejecutado el siguiente comando para instalarla:

``` bash
sudo apt-get install lm-sensors
```

Una vez instalada he ejecutado los siguientes comandos para configurarla y arrancarla:

``` bash
sudo sensors-detect
sudo service kmod start
```

##### Información adicional
[lm-sensors](http://www.lm-sensors.org/)  
[Repositorio Github](https://github.com/groeck/lm-sensors)  
[How do I get the CPU temperature?](http://askubuntu.com/questions/15832/how-do-i-get-the-cpu-temperature)

####  smartmontools

Para obtener la información de los discos se puede utiliar el paquete smartmontools:

``` bash
apt-get install smartmontools
```

####  hddtemp

Para obtener la información de los discos se puede utilizar el paquete hddtemp:

``` bash
apt-get install hddtemp
```



## Instalación de la web de monitorización

### Instalación de la web

Los pasos para instalar el proyecto en la Cubieboard son los siguientes:

* Configurar git, sólo la primera vez:

``` bash
git config --global user.email "correo"
git config --global user.name "usuario"
```

* Bajar el proyecto desde github a la carpeta ~/cubieboard-monitor:

``` bash
cd
git clone https://github.com/juaalta/cubieboard-monitor.git cubieboard-monitor
```

* Entrar en la carpeta en la que se ha descargado e instalar las dependencias necesarias:

``` bash
cd cubieboard-monitor

npm install
```

Una vez seguidos los pasos anteriores, si queremos probar la aplicación sólo tenemos que lanzar el siguiente comando:

``` bash
nodejs server.js
```

También puede ejecutarse:

``` bash
npm start
```
