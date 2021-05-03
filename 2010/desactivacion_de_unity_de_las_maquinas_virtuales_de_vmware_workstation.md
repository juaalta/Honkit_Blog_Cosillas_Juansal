# Desactivación de Unity de las máquinas virtuales de VMware Workstation

Al desactivar el unity de las máquinas vituales conseguimos que la carpeta cache que ha aparecido desde la versión 7.1 desaparezca.

En el fichero `config.ini` hay que introducir/modificar la siguiente línea:

```
isolation.tools.unity.disable = "true"
```

En el fichero vmx de la máquina virtual:

```
unity.enableLaunchMenu = "FALSE"
unity.showBadges = "FALSE"
unity.showBorders = "FALSE"
unity.wasCapable = "FALSE"
```
