# Máquina virtual para trabajar con documentos en Markdown - Nueva versión

Después de estar trabajando con markdown durante un tiempo he ido actualizando y renovando las aplicaciones que utilizo. Por esto me he decido a volver a crear la máquina virtual desde cero, de esta forma aprovecho para actualizar tanto el sistema operativo, como las aplicaciones que utilizo.

## Información sobre el sistema operativo.

He instalado la distribución Fedora 23 con el escritorio LXDE.

Adicionalmente he actualizado el gestor de paquetes de yum a dnf, para esto he ejecutado los siguientes comandos:

``` bash
sudo dnf install python-dnf-plugins-extras-migrate && dnf-2 migrate
```

## Instalación de utilidades que yo considero necesarias.

Las utilidades que considero necesarias dentro del sistema operativo y que no son las que permiten trabajar directamente con Markdown son las siguientes:

### Yumex

Como gestor de paquetes he elegido a Yumex.
Para esto he ejecutado los siguientes comandos:

``` bash
sudo dnf install yumex
```

### Firefox

Para navegar y poder visualizar los documentos generados como web o website he elegido Firefox.
Para esto he ejecutado los siguientes comandos:

``` bash
sudo dnf install firefox
```

### Gimp

Como editor de imágenes he elegido Gimp.
Para esto he ejecutado los siguientes comandos:

``` bash
sudo dnf install gimp
```

### Servidor FTP

Como servidor de FTP para subir y bajar los ficheros a la máquina virtual he elegido el vsftp.
Para esto he ejecutado los siguientes comandos:

``` bash
sudo dnf install vsftpd
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

Como cliente de FTP he elegido el FileZilla.
Para esto he ejecutado los siguientes comandos:

``` bash
sudo dnf install filezilla
```

### GIT

Para acceder a los documentos guardados en GitHub he instalado el cliente de Git.
Para esto he ejecutado los siguientes comandos:

``` bash
sudo dnf install git
```


### Sublime text

Como editor general de textos he elegido el Sublime Text.
Para esto he seguido los siguientes pasos:

He descargado la versión 2 de: [http://www.sublimetext.com/2](http://www.sublimetext.com/2)

Después he ejecutado los siguientes comandos:

``` bash
tar vxjf Sublime\ Text\ 2.0.2\ x64.tar.bz2
sudo mv Sublime\ Text\ 2 /opt/
sudo ln -s /opt/Sublime\ Text\ 2/sublime_text /usr/bin/sublime
```

Para la creación del fichero de acceso directo he seguido los siguientes pasos:

He creado el siguiente fichero desde el mismo sublime, ejecutando el siguiente comando:

``` bash
sudo sublime /usr/share/applications/sublime.desktop
```

Dentro del fichero he insertado los siguientes dagos:

``` ini
[Desktop Entry]
Version=2.0.2
Name=Sublime Text 2
# Only KDE 4 seems to use GenericName, so we reuse the KDE strings.
# From Ubuntu's language-pack-kde-XX-base packages, version 9.04-20090413.
GenericName=Text Editor

Exec=sublime
Terminal=false
Icon=/opt/Sublime Text 2/Icon/48x48/sublime_text.png
Type=Application
Categories=TextEditor;IDE;Development
X-Ayatana-Desktop-Shortcuts=NewWindow

[NewWindow Shortcut Group]
Name=New Window
Exec=sublime -n
TargetEnvironment=Unity
```

## Instalación y uso de las utilidades de Markdown

### Haroopad

Para mí es el editor que uso a diario, con el que genero la mayoría de la documentación.

#### Requerimientos previos

Se ha de instalar la siguiente librería:

``` bash
sudo dnf install systemd-libs.i686 -y
```

#### Instalación de haroopad

El paquete de instalación lo he descarado desde la [página de Haroopad](http://pad.haroopress.com/user.html).
El link de descarga que he utilizado es: [Linux Binary (64bit)](https://bitbucket.org/rhiokim/haroopad-download/downloads/haroopad-v0.13.1-x64.tar.gz)

Los comandos que he utilizado para realizar la instalación son:

``` bash
tar zxvf haroopad-v0.13.1-x64.tar.gz

tar -zxvf data.tar.gz
sudo cp -R ./usr /

tar zxf control.tar.gz
chmod 755 postinst
sudo ./postinst
```

Para solucionar el problema de que no se ve el icono se han de realizar las siguientes modificaciones en el fichero `/usr/share/applications/Haroopad.desktop`.
Se ha de reemplazar la linea `Icon=haroopad` por `Icon=/usr/share/icons/hicolor/128x128/apps/haroopad.png`.

#### Uso

Es un cliente gráfico, no necesita usar la línea de comandos para su funcionamiento.

#### Información adicional

[Página oficial de haroopad](http://pad.haroopress.com/user.html)

[Blog con información de como instalar el Haroopad en Fedora](http://www.bonashen.com/post/artifice/20140805-install-haroopad-on-fedora-20-64bit)

### Gitbook

Es el editor que uso para tener todo el contenido del blog o parte de el de forma offline y de libro.
La versión en el momento de la redacción del documento es la 2.5.2.

#### Requerimientos previos

##### Node.js
Para poder instalar el Gitbook se ha de instalar el gestor de paquetes de Node.js npm. Para instalarlo he ejecutado el siguiente comando:

``` bash
sudo dnf install npm
```

##### Calibre

Para poder generar los libros en cualquier formato no web se necesita Calibre. Para instalarlo he ejecutado el siguiente comando:

``` bash
sudo dnf install calibre
```

#### Instalación de gitbook desde npm

Para instalar el Gitbook desde el npm se ha de ejecutar el siguiente comando:

``` bash
sudo npm install gitbook-cli -g
```

#### Uso

Para trabajar con los documentos con gitbook he creado la siguiente carpeta:

```
/home/juansal/gitbook
```

##### Inicializar un libro vacío:

Para inicializar un libro vacío se puede hacer de 2 formas diferentes:

1. Crear una carpeta para contener el libro, entrar en ella y ejecutar el siguiente comando:
``` bash
gitbook init
```

2. Ejecutar el siguiente comando que crea la carpeta directamente:
``` bash
gitbook init ./carpeta
```

###### Opciones disponibles:

```
  init [directory] 	 create files and folders based on contents of SUMMARY.md
```

##### Previsualizar y servir un libro:

Para previsualizar y servir un libro se puede hacer de 2 formas diferentes:
1. Desde dentro de la carpeta del libro:
``` bash
gitbook serve
```

2. Desde fuera de la carpeta del libro:
``` bash
gitbook serve ./repository
```

###### Opciones disponibles:

```
  serve [book] 	 Build then serve a gitbook from a directory
    --port 	 Port for server to listen on (Default is 4000)
    --lrport 	 Port for livereload server to listen on (Default is 35729)
    --watch 	 Enable/disable file watcher (Default is true)
    --format 	 Format to build to (Default is website; Values are website, json, ebook)
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)
```

##### Generar web estática:

1. Desde dentro de la carpeta del libro:
``` bash
gitbook build
```
2. Desde fuera de la carpeta del libro:
``` bash
gitbook build ./repository
```

###### Opciones disponibles:

```
  build [book] [output] 	 build a book
    --format 	 Format to build to (Default is website; Values are website, json, ebook)
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)
```

##### Generar pdf:

1. Desde dentro de la carpeta del libro:
``` bash
gitbook pdf
```
2. Desde fuera de la carpeta del libro:
``` bash
gitbook pdf ./repository
```

###### Opciones disponibles:

```
  pdf [book] [output] 	 build a book to pdf
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)
```

##### Generar epub:

1. Desde dentro de la carpeta del libro:
``` bash
gitbook epub
```
2. Desde fuera de la carpeta del libro:
``` bash
gitbook epub ./repository
```

###### Opciones disponibles:

```
  epub [book] [output] 	 build a book to epub
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)
```

##### Generar mobi:

1. Desde dentro de la carpeta del libro:
``` bash
gitbook mobi
```
2. Desde fuera de la carpeta del libro:
``` bash
gitbook mobi ./repository
```

###### Opciones disponibles:

```
  mobi [book] [output] 	 build a book to mobi
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)
```

##### Ayuda completa de gitbook desde línea de comandos

Comando ejecutado:

``` bash
gitbook
```

Resultado obtenido:

```
  Usage: gitbook [options] [command]


  Commands:

    versions                          list installed versions
    versions:print                    print current version to use in the current directory
    versions:available                list available versions on NPM
    versions:install [version]        force install a specific version of gitbook
    versions:link [folder] [version]  link a version to a local folder
    versions:uninstall [version]      uninstall a specific version of gitbook
    versions:update [tag]             update to the latest version of gitbook
    help                              list commands for a specific version of gitbook
    *                                 run a command with a specific gitbook version

  Options:

    -h, --help               output usage information
    -V, --version            output the version number
    -v, --gitbook [version]  specify GitBook version to use
    -d, --debug              enable verbose error
```

Comando ejecutado:

``` bash
gitbook help
```

Resultado obtenido:

```
  build [book] [output] 	 build a book
    --format 	 Format to build to (Default is website; Values are website, json, ebook)
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)

  pdf [book] [output] 	 build a book to pdf
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)

  epub [book] [output] 	 build a book to epub
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)

  mobi [book] [output] 	 build a book to mobi
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)

  serve [book] 	 Build then serve a gitbook from a directory
    --port 	 Port for server to listen on (Default is 4000)
    --lrport 	 Port for livereload server to listen on (Default is 35729)
    --watch 	 Enable/disable file watcher (Default is true)
    --format 	 Format to build to (Default is website; Values are website, json, ebook)
    --log 	 Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)

  install [book] 	 install plugins dependencies

  init [directory] 	 create files and folders based on contents of SUMMARY.md
```

#### Información adicional

[https://github.com/GitbookIO/gitbook/](https://github.com/GitbookIO/gitbook/)

### Gitbook Editor Legacy

Este editor está descontinuado, pero funciona perfectamente para la versión de Gitbook indicada en este documento. Este editor me permite ver como quedaran los documentos antes de generarlos y de esta forma evitar tener que generar el documento para ver como quedará después de generado.

#### Requerimientos previos

##### Calibre

Para poder generar los libros en cualquier formato no web se necesita Calibre. Para instalarlo he ejecutado el siguiente comando:

``` bash
sudo dnf install calibre
```

#### Instalación de gitbook editor legacy

1. Descargar el instalable desde la siguiente ruta: [https://github.com/GitbookIO/editor-legacy/releases](https://github.com/GitbookIO/editor-legacy/releases)
2. Descomprimir usando:
 ``` bash
 tar zxvf gitbook-linux64.tar.gz
 ```
3. Renombrar y mover la carpeta de gitbook editor:
``` bash
mv linux64 gitbook-editor
mv gitbook-editor ..
```
4. Por un bug en la referencia a una librería se ha de ejecutar el siguiente comando:
``` bash
sudo ln -sf /lib64/libudev.so.1 /lib64/libudev.so.0
```
5. Arranque del script de instalación:
``` bash
cd gitbook-editor
chmod +x *.sh
./install.sh
```
4. Ahora hay un icono en el menú inicio
5. Abrirlo y empezar


#### Uso

Es un cliente gráfico, no necesita usar la línea de comandos.

#### Información adicional

[Página de github de Gitbook Editor Legady](https://github.com/GitbookIO/editor-legacy/)

### Gitbook Editor

Este editor es la evolución del anterior y tiene conexión con los libros publicados en GitBook. Lo que no me gusta es la necesidad de git para poder crear libros que no desees subir a GitBook y tenerlos solamente en local.

Este editor no lo he instalado en mi máquina por no tener paquetes rpm para su instalación.


#### Información adicional

[Página de github de Gitbook Editor](https://www.gitbook.com/editor)

### Leanpub

Esta herramienta es completamente web y no tiene cliente por línea de comandos ni offline.
Aunque es anterior a Gitbook la conocí después y la uso para lo mismo que ésta, para poder tener el blog de forma offline y de libro.
En mi caso genero los documentos en local y los subo mediante github. Después desde la web pido la generación del documento.

#### Información adicional

[Página oficial de Leanpub](https://leanpub.com/)

[Manual online de Leanpub](https://leanpub.com/help/manual)

### Easybook

Este es el último de los generadores de documentos, a partir de Markdown, que conocí. En mi caso me gusta bastante para generar documentación compleja en formato web, me permite generar esta en un sólo documento html o en formato página web.

#### Requerimientos previos

Los requerimientos previos son los siguientes:

- PHP
- Composer

Los requerimientos complementarios son los siguientes:

- PrinceXML
- Kindlegen

##### PHP

Para instalar el php se ha de ejecutar el siguiente comando:

``` bash
sudo dnf install php
```

##### Composer

Para instalar composer he ejecutado los siguientes comandos:

``` bash
curl -sS https://getcomposer.org/installer | php -- --install-dir=/home/juansal --filename=composer
sudo cp composer /usr/bin
```

Información adicional de composer en su [página oficial](https://getcomposer.org/).

##### PrinceXML

Para instalar PrinceXML he descargado desde el navegador el siguiente fichero:  [CentOS 7 / 64-bit rpm](http://www.princexml.com/download/prince-10r5-1.centos7.x86_64.rpm) y le he indicado a este que lo abra con el yumex, de esta forma este último instalará el paquete con sus dependencias.

Información adicional de PrinceXML en su [página oficial](http://www.princexml.com/)

##### Kindlegen

Para descargar Kindlegen me he conectado a la [página de este](http://amzn.to/kindlegen) y desde ella he descargado el link: **KindleGen v2.9 for Linux 2.6 i386** sobre la carpeta **~/Descargas/**.

Después de descargar el fichero he creado la carpeta **~/kindlegen**.

``` bash
mkdir ~/kindlegen
```

He entrado en la carpeta creada y descomprimido el fichero descargado.

``` bash
cd ~/kindlegen
tar zxvf ~/Descargas/kindlegen_linux_2.6_i386_v2_9.tar.gz
```

#### Instalación de Easybook

Para instalar Easybook se ha de lanzar el siguiente comando:

``` bash
composer create-project easybook/easybook easybook
```

Una forma de saber si se ha instalado de forma correcta el programa se puede lanzar el siguiente comando:

``` bash
./book
```

Si no dá un error el resultado de la ejecución de éste es similar a lo siguiente:

```
                     |              |
 ,---.,---.,---.,   .|---.,---.,---.|__/
 |---',---|`---.|   ||   ||   ||   ||  \
 `---'`---^`---'`---|`---'`---'`---'`   `
                `---'

easybook is the easiest and fastest tool to generate
technical documentation, books, manuals and websites.

Available commands:
  benchmark   Benchmarks the performance of book publishing
  customize   Eases the customization of the book design
  help        Displays help for a command
  list        Lists commands
  new         Creates a new empty book
  publish     Publishes an edition of a book
  version     Shows installed easybook version

```


#### Uso

Para trabajar con los documentos con easybook he creado la siguiente carpeta:

```
/home/juansal/easybook
```

##### Inicializar un libro vacío:

Para inicializar un libro vacío se ha de lanzar el siguiente comando:

``` bash
./book new "Titulo del libro"
```

##### Generar un libro en formato html

Para generar el libro en formato html se ha de ejecutar el siguiente comando:

``` bash
./book publish Titulo-del-libro web
```

##### Generar un libro en formato web

Para generar el libro en formato várias páginas en html se ha de ejecutar el siguiente comando:

``` bash
./book publish Titulo-del-libro website
```

##### Generar un libro en formato epub

Para generar el libro en formato epub se ha de ejecutar el siguiente comando:

``` bash
./book publish Titulo-del-libro ebook
```

##### Generar un libro en formato mobi

Para generar el libro en formato mobi se ha de ejecutar el siguiente comando:

``` bash
./book publish Titulo-del-libro kindle
```

##### Generar un libro en formato pdf

Para generar el libro en formato pdf se ha de ejecutar el siguiente comando:

``` bash
./book publish Titulo-del-libro print
```


#### Información adicional

[Página oficial de easybook](http://easybook-project.org/)

[Página de github de easybook](https://github.com/javiereguiluz/easybook)

