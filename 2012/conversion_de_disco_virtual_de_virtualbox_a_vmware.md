# Conversión de disco virtual de VirtualBox a VMware

Los pasos a seguir para la conversión del disco virtual de la máquina de VirtualBox son los siguientes:
- Entrar en la carpeta en la que se encuentra el disco virtual a convertir.
- Ejecutar el siguiente comando (para esto ha de estar el VirtualBox instalado):
``` bash
"c:\Program Files\Oracle\VirtualBox\VBoxManage.exe" clonehd DiscoOrigen.vdi DiscoDestino.vmdk  --format vmdk --variant standard
```


Este comando es de consola, por tanto no se puede ejecutar desde entorno gráfico.

**DiscoOrigen.vdi** es el disco en VirtualBox, el origen.

**DiscoDestomp.vmdk** es el disco destino en VMware.

La ruta que ejecuta el `VBoxManage.exe`, en el ejemplo, es la por defecto de la instalación y puede cambiar.

