# Añadir a un usuario los permisos de `sudo` en Fedora

Puede hacerse de 2 formas distintas:

## Añadiendo al usuario los permisos directamente

Para esta opción hay que realizar los siguientes pasos:

* Ejecutar como root el siguiente comando:
``` bash
visudo
```
* Añadir la siguiente línea:
```
usuario    ALL=(ALL)       ALL
```
debajo de la línea:
```
root    ALL=(ALL)       ALL
```

## Añadir al usuario al grupo wheel

Para esta opción hay que realizar los siguientes pasos:

* Ejecutar como root los siguientes comandos:
``` bash
gpasswd wheel -a usuario
visudo
```
* Descomentar la línea, si esta comentada:
```
%wheel  ALL=(ALL)       ALL
```
