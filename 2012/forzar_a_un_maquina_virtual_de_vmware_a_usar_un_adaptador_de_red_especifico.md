# Forzar a un máquina Virtual de VMware a usar un adaptador de red específico

Para hacer esto existen 2 formas distintas, estas son:

## Modificar el fichero vmx a mano:

Se han de añadir/modificar las siguientes líneas, ya que por defecto el VMware usa el vmnet0:

```
ethernet0.connectionType = "custom"
ethernet0.vnet = "VMnet2"
```


En este caso el VMnet2 ha de estar creado y asignado a una tarjeta de red, si no, esta solución no funciona.

## Utilizar el Virtual Network Editor: (Lo que se indica en este punto sólo funciona hasta la versión 5 del VMware Player)

En este programa hay que cambiar las opciones automáticas del vmnet0 para que seleccione el adaptador que deseemos.
Si tenemos el VMware Player este programa no se instala, pero hay una forma de instalarlo, ya que sí que se encuentra dentro del instalable. Para hacer esto se han de seguir los siguientes pasos:
* Descomprimir el instalable mendiante el comando: `VMware-player-4.0.1-528992.exe /e .\extract`
* Entrar en la carpeta *extract* y buscar el fichero *network.cab*.
* Del fichero este obtener el fichero *vmnetcfg.exe*,
* Mover este último a la carpeta en la que se haya instalado el VMware Player.
* Crear un acceso directo a este último (esto es opcional).

A partir de la versión 6 del VMware Player esto ya no puede hacerse, ya que estos ficheros no están, han de obtenerse desde un VMware Workstation.
