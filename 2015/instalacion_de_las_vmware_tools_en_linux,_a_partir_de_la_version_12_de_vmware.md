# Instalación de las vmware tools en linux, a partir de la versión 12 de VMware

## Información sobre la instalación de las vmware tools

A partir de esta versión de vmware, si intentas instalar las vmware tools lo primero que te recomienda el instalador es que no instales las que lleva el entorno y que te instales las open-vm-tools.

[Página de VMware con la información](http://kb.vmware.com/kb/2073803)

[Página del proyecto en sourceforge](http://sourceforge.net/projects/open-vm-tools/)

[Página del proyecto en github](https://github.com/vmware/open-vm-tools)

## Comandos para realizar la instalación

### UBUNTU / DEBIAN

El comando a ejecutar para realizar la instalación es el siguiente:

``` bash
sudo apt-get install open-vm-tools
```

Si se dispone de entorno gráfico instalado, se ha de ejecutar también el siguiente comando:

``` bash
sudo apt-get install open-vm-tools-desktop
```

### CENTOS / FEDORA / RED-HAT

El comando a ejecutar para realizar la instalación es el siguiente:

``` bash
sudo yum install open-vm-tools
```

Si se dispone de entorno gráfico instalado, se ha de ejecutar también el siguiente comando:

``` bash
sudo yum install open-vm-tools-desktop
```
