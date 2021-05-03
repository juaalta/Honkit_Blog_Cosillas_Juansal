# Cambiar el propietario y el grupo al que pertenece un fichero o una carpeta en linux

## Propietario
Para cambiar el propietario de un fichero se utiliza el siguiente comando:
``` bash
chown Nuevo_Propietario fichero
```

Para cambiar el propietario de una carpeta:
``` bash
chown Nuevo_Propietario carpeta
```

Para cambair el propietario de una carpeta y su contenido de forma recursiva:
``` bash
chown -R Nuevo_Propietario carpeta
```

## Grupo
Para cambiar el grupo de un fichero se utiliza el siguiente comando:
``` bash
chgrp Nuevo_Grupo fichero
```

Para cambiar el grupo de una carpeta:
``` bash
chgrp Nuevo_Grupo carpeta
```

Para cambair el grupo de una carpeta y su contenido de forma recursiva:
``` bash
chgrp -R Nuevo_Grupo carpeta
```

## Propietario y grupo
Para cambiar el propietario y el grupo de un fichero se utiliza el siguiente comando:
``` bash
chown Nuevo_Propietario:Nuevo_Grupo fichero
```

Para cambiar el propietario y el grupo de una carpeta:
``` bash
chown Nuevo_Propietario:Nuevo_Grupo carpeta
```

Para cambair el propietario y el grupo de una carpeta y su contenido de forma recursiva:
``` bash
chown -R Nuevo_Propietario:Nuevo_Grupo carpeta
```
