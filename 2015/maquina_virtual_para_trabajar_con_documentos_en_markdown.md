# Máquina virtual para trabajar con documentos en Markdown

Para trabajar con Markdown me he creado una máquina virtual con los siguientes programas.

## Información sobre el sistema operativo.

Se ha instalado la distribución Fedora con el escritorio LXDE.

## Instalación de utilidades que yo considero necesarias.

### Yumex

``` bash
yum install yumex
```

### Firefox

``` bash
yum install firefox
```

### Gimp

``` bash
yum install gimp
```

### Servidor FTP

``` bash
yum install vsftpd
```

Después de instalar el servidor de ftp se ha de activar en el firewall el servicio ftp, para que este sea accesible desde fuera de la máquina.

Los cambios realizados en el fichero de configuración del vsftpd (/etc/vsfptd/vsftpd.conf) son:

```
anonymous_enable=NO
```

También he desactivado el selinux (/etc/selinux/config), por que voy a trabajar en local y dentro de una máquina virtual.

```
SELINUX=disabled
```

Después de esto hay que reiniciar para que el selinux se desactive.

### Cliente FTP

``` bash
yum install filezilla
```

### GIT

``` bash
yum install git
```

### Subversion

``` bash
yum install svn
```

## Instalación de editores de Markdown

### Gitbook 1.5.0

Esta es la vesión final en el momento de la redacción del documento.

#### Requerimientos previos

``` bash
yum install npm
```

#### Instalación de gitbook desde npm

``` bash
npm install gitbook -g
```

#### Uso

##### Generar libro:

``` bash
gitbook serve ./repository
```

##### Generar web estática:

``` bash
gitbook build ./repository --output=./outputFolder
```

##### Opciones disponibles:

```
-o, --output <directory>  Path to output directory, defaults to ./_book
-f, --format <name>       Change generation format, defaults to site, availables are: site, page, ebook, json
--config <config file>    Configuration file to use, defaults to book.js or book.json
```

##### Modo debug al generar libro:

``` bash
export DEBUG=true
gitbook build ./
```

#### Información adicional

[https://github.com/GitbookIO/gitbook/](https://github.com/GitbookIO/gitbook/)

### Gitbook Editor

Este editor está descontinuado, pero funciona perfectamente para la versión de Gitbook indicada en este documento. Además de esto yo prefiero poder editar mis documentos en local y después subirlos a la web.

#### Requerimientos previos

``` bash
yum install calibre
```

#### Instalación de gitbook editor

1. Descargar el instalable desde la siguiente ruta: [https://github.com/GitbookIO/editor/releases](https://github.com/GitbookIO/editor/releases)
2. Descomprimir usando:
 ``` bash
 tar zxvf gitbook-linux64.tar.gz
 ```
3. Renombrar y mover la carpeta de gitbook editor:
``` bash
mv linux64 gitbook
mv gitbook ..
```
4. Por un bug en la referencia a una librería se ha de ejecutar el siguiente comando:
``` bash
sudo ln -sf /lib64/libudev.so.1 /lib64/libudev.so.0
```
5. Arranque del script de instalación:
``` bash
cd gitbook
chmod +x *.sh
./install.sh
```
4. Ahora hay un icono en el menú inicio
5. Abrirlo y empezar


#### Uso

Es un cliente gráfico, no necesita usar la línea de comandos.

#### Información adicional

[Página de github de Gitbook Editor](https://github.com/GitbookIO/editor)

### Haroopad

#### Requerimientos previos

Se ha de instalar la siguiente librería:

sudo yum install systemd-libs.i686 -y

#### Instalación de haroopad

Hemos de descargarlo desde la [página de Haroopad](http://pad.haroopress.com/user.html).
El link de descarga que he utilizado es: [Linux Binary (64bit)](https://bitbucket.org/rhiokim/haroopad-download/downloads/haroopad-v0.13.0_x64.tar.gz)

Los comandos a ejecutar para realizar la instalación son:
``` bash
tar -zxvf haroopad-v0.12.2_amd64.tar.gz
tar -zxvf data.tar.gz
sudo cp -R ./usr /

tar zxf control.tar.gz
chmod 755 postinst
sudo ./postinst
```

Para solucionar el problema de que no se ve el icono se han de realizar las siguientes modificaciones en el fichero `/usr/share/applications/Haroopad.desktop`.
Se ha de reemplazar `Icon=haroopad` por `Icon=/usr/share/icons/hicolor/128x128/apps/haroopad.png`.


#### Uso

Es un cliente gráfico, no necesita usar la línea de comandos.

#### Información adicional

[Página de haroopad](http://pad.haroopress.com/user.html)

[Blog con información de como instalar el Haroopad en Fedora](http://www.bonashen.com/post/artifice/20140805-install-haroopad-on-fedora-20-64bit)
