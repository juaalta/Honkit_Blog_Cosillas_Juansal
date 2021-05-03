# Máquina virtual de desarrollo para proyectos de AngularJS y NodeJS

Intentando afianzar mis conocimientos de AngularJS y NodeJS me he creado esta máquina virtual. En ella crearé todos los proyectos que usen estos frameworks de Javascript.

## Información sobre máquina virtual

Esta máquina virtual la he creado con el VMware Player 12.

### Características del hardware

La configuración del hardware usada ha sido la siguiente:

- Memoria: 4Gb RAM.
- Procesador: 1 procesador con 2 cores
- Disco duro: disco SCSI de 40Gb, con fichero único autoexpandible.
- CD-ROM: Usando unidad física, salvo en el momento de la instalación que se le ha asignado la imagen ISO del sistema operativo.
- Adaptador de red: NAT.
- Un controlador USB.
- Pantalla.

El resto de hardware que se hubiera añadido de forma automática lo he eliminado.

### Información sobre el sistema operativo

He instalado la distribución Fedora 23 de 64 bits con el escritorio LXDE.
Adicionalmente he actualizado el gestor de paquetes de **yum** a **dnf**, para esto he ejecutado los siguientes comandos:

``` bash
sudo dnf install python-dnf-plugins-extras-migrate && dnf-2 migrate
```

Después de esto he actualizado el sistema operativo, para esto he ejecutado los siguientes comandos:

``` bash
sudo dnf update
```

## Instalación de utilidades que yo considero necesarias.

Las utilidades que considero necesarias dentro del sistema operativo y que no son las que permiten trabajar directamente con los frameworks son las siguientes:

### Terminator

Como terminal he instalado esta herramienta, la cual me permite trabajar tanto a pantalla partida como con diferentes pestañas.  
Para la instalación he ejecutado los siguientes comandos:

``` bash
sudo dnf install terminator
```

#### Información adicional

[Terminator](https://launchpad.net/terminator)

### Navegadores

Para navegar y poder visualizar los proyectos generados he decidido instalar Firefox y Chrome.

#### Firefox

Para la instalación he ejecutado los siguientes comandos:

``` bash
sudo dnf install firefox
```

#### Chrome

Para la instalación he seguido los siguientes pasos:

* Cambiar a root:

``` bash
su -
```

* Después de esto he ejecutado el siguiente comando:

``` bash
cat << EOF > /etc/yum.repos.d/google-chrome.repo
[google-chrome]
name=google-chrome - \$basearch
baseurl=http://dl.google.com/linux/chrome/rpm/stable/\$basearch
enabled=1
gpgcheck=1
gpgkey=https://dl-ssl.google.com/linux/linux_signing_key.pub
EOF
```

* Para completar la instalación he ejecutado el siguiente comando:

``` bash
dnf install google-chrome-stable
```

##### Información adicional

[Install Google Chrome on Fedora 24/23, CentOS/RHEL 7.2](http://www.if-not-true-then-false.com/2010/install-google-chrome-with-yum-on-fedora-red-hat-rhel/)

### Filezilla

Como cliente de FTP he elegido el FileZilla.  
Para la instalación he ejecutado los siguientes comandos:

``` bash
sudo dnf install filezilla
```

### Haroopad

Para mí es el editor que uso a diario y con el que genero la mayoría de la documentación.

#### Requerimientos previos

Se ha de instalar la siguiente librería:

``` bash
sudo dnf install systemd-libs.i686 -y
```

#### Instalación de haroopad

El paquete de instalación lo he descarado desde la [página de Haroopad](http://pad.haroopress.com/user.html).  
El link de descarga que he utilizado es: [Linux Binary (64bit)](https://bitbucket.org/rhiokim/haroopad-download/downloads/haroopad-v0.13.1-x64.tar.gz) y la descarga la he realizado dentro del directorio `~/Descargas`

Los comandos que he utilizado para realizar la instalación son:

``` bash
cd ~/Descargas

tar zxvf haroopad-v0.13.1-x64.tar.gz

tar -zxvf data.tar.gz
sudo cp -R ./usr /

tar zxf control.tar.gz
chmod 755 postinst
sudo ./postinst
```

Para solucionar el problema de que no se ve el icono se han de realizar las siguientes modificaciones en el fichero `/usr/share/applications/Haroopad.desktop`.
Se ha de reemplazar la linea `Icon=haroopad` por `Icon=/usr/share/icons/hicolor/128x128/apps/haroopad.png`.


### atom

Como editor de código he elegido a [atom](http://atom.io) por su simplicidad y su capacidad de ampliarse con plugins.

#### Instalación:

El paquete de instalación lo he descarado desde la [página de atom](http://atom.io).  
El link de descarga que he utilizado es: [https://atom.io/download/rpm](https://atom.io/download/rpm) y la descarga la he realizado dentro del directorio `~/Descargas`

Los comandos que he utilizado para realizar la instalación son:

``` bash
cd ~/Descargas
sudo rpm -ivh atom.x86_64.rpm
```

En caso de error por dependencias se puede instalar ejecutando los siguientes comandos:

``` bash
cd ~/Descargas
sudo dnf install atom.x86_64.rpm
```

#### plugins atom

Los plugins que he instalado dentro de atom han sido los siguientes:

* AngularJS support in Atom
* atom-beautify
* atom-formatter-jsbeautify
* Markdown preview

### Control de versiones

Como control de versiones voy a usar git, ya que mi intención es publicar sobre github.

Para acceder a los proyectos guardados en GitHub he instalado los siguientes clientes de Git.

#### Git

Este es el cliente usado para cuando quiera trabajar por línea de comandos.  
Para la instalación he ejecutado los siguientes comandos:

``` bash
sudo dnf install git
```

#### SmartGit

Como cliente gráfico he elegido [SmartGit](http://www.syntevo.com/smartgit/).

##### Requerimientos

Se ha de instalar java:

``` bash
sudo dnf install java
```

##### Instalación:

El paquete de instalación lo he descarado desde la [página de SmartGit](http://www.syntevo.com/smartgit/).  
El link de descarga que he utilizado es: [http://www.syntevo.com/smartgit/download?file=smartgit/smartgit-linux-7_1_2.tar.gz](http://www.syntevo.com/smartgit/download?file=smartgit/smartgit-linux-7_1_2.tar.gz) y la descarga la he realizado dentro del directorio `~/Descargas`

Los comandos ejecutados para la instalación han sido

``` bash
cd ~/Descargas
tar zxvf smartgit-linux-7_1_2.tar.gz -C /tmp/
sudo mv /tmp/smartgit /opt/
sudo ln -s /opt/smartgit/bin/smartgit.sh /usr/local/bin/smartgit

sudo /opt/smartgit/bin/add-menuitem.sh
```

#### Información adicional:

http://tutorialforlinux.com/2014/12/10/how-to-install-smartgit-client-on-fedora-32-64bit-linux/
http://tutorialforlinux.com/2014/12/10/how-to-create-a-smartgit-linux-desktop-menu-launcher-easy-guide/

## Instalación de AngularJS y NodeJS

### AngularJS

No requiere instalación.

#### Información adicional
https://angularjs.org/
https://carlosazaustre.es/blog/empezando-con-angular-js/
https://carlosazaustre.es/blog/tutorial-ejemplo-de-aplicacion-web-con-angular-js-y-api-rest-con-node/

### NodeJS

Para la instalación de [NodeJS](https://nodejs.org/) he elegido la última versión (en el momento de escribir el artículo es la 6.x) y he ejecutado los siguientes comandos:

``` bash
su -
curl --silent --location https://rpm.nodesource.com/setup_6.x | bash -
dnf -y install nodejs npm gcc-c++ make
```

##### Información adicional

[Installing Node.js via package manager](https://nodejs.org/en/download/package-manager/#enterprise-linux-and-fedora)

### bower

Los comandos que he utilizado para realizar la instalación de [Bower](https://bower.io/) son:

``` bash
npm install -g bower
```

### Grunt

Los comandos que he utilizado para realizar la instalación de [Grunt](http://gruntjs.com/) son:

``` bash
npm install -g grunt-cli
```
