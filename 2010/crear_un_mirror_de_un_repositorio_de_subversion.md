# Crear un mirror de un repositorio de subversion

Para crear un mirror de un repositorio de subversion se siguen los siguientes pasos.
La mayoria de los pasos se hacen sobre el mirror.

Creamos el repositorio en la máquina del mirror.
Creamos un usuario en ambos servidores para realizar la sincronización (en este ejemplo el usuario creado ha sido: syncuser)
Lanzamos los siguientes comandos en el mirror:

``` bash
svnsync initialize file:///ruta_local_mirror  ruta_servidor_svn --username syncuser --password syncuser
svn proplist --revprop -r 0 file:///ruta_local_mirror
svn propget svn:sync-from-url --revprop -r 0 file:///ruta_local_mirror
svn propdel svn:sync-lock --revprop -r 0 file:///ruta_local_mirror
```

Con esto ya tenemos el mirror montado y preparado para funcionar. Un comando interesante a ejecutar, aunque no necesario, es el siguiente, el cual se encarga de la sincronización inicial de los repositorios. Como he dicho no es necesario, pero si el repositorio del que vamos a hacer el mirror ya contiene información es recomendable, especialmente si este ya tiene muchos commits realizados.
``` bash
svnsync --non-interactive sync file:///ruta_local_mirror --username syncuser --password syncuser
```
Después de esta sincronización inicial es conveniente ejecutar el siguiente comando para que se copien las propiedades del repositorio (sólo es necesario esta primera vez):
``` bash
svnsync copy-revprops file:///ruta_local_mirror --username syncuser --password syncuser
```

Después de esto en el repositorio origen del subversion se puede crear un hook para que la sincronización se realice de forma automática, el hook en el que incluir el siguiente comando es el post_commit:
``` bash
svnsync --non-interactive sync ruta_trabajo_mirror --username syncuser --password syncuser
```
