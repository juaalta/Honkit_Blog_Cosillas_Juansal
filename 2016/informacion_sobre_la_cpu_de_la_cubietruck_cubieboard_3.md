# Información sobre la CPU de la cubietruck (cubieboard 3)

## Finalidad de artículo

La finalidad de este artículo es ampliar la información sobre el estado de la cubietruck que [creé anteriormente](../2014/informacion_sobre_temperatura_y_discos_duros_en_la_cubietruck_cubieboard_3.md) y ampliar la información a mostrar en la web generada en el [artículo anterior](../2015/web_con_informacion_sobre_temperatura_y_discos_duros_en_la_cubietruck_cubieboard_3.md).

## Nuevos comandos instalados

### htop

htop es un visor de procesos interactivo para Linux. Es una aplicación en modo texto (para consola o terminales X) y requiere ncurses.

``` bash
apt-get install htop
```

## Scripts adicionales con información de CPU y memoria

### Información del uso de CPU global:

El nombre usado para el script ha sido `val_CPU.sh` y se ha guardado dentro de `/home/linaro/scripts`.

El script realiza 2 lecturas del fichero `/proc/stat` con una diferencia de tiempo de 1 segundo, de esta forma resta las dos lecturas y devuelve el uso de CPU durante el último segundo. La variable que consulta es `cpu`.

#### Contenido del script

``` bash
#!/bin/bash

function valor_USUARIO ()
{
	CPU_AUX=$2
	echo $CPU_AUX
}

function valor_NICE ()
{
	CPU_AUX=$3
	echo $CPU_AUX
}

function valor_SISTEMA ()
{
	CPU_AUX=$4
	echo $CPU_AUX
}

function valor_IDLE ()
{
	CPU_AUX=$5
	echo $CPU_AUX
}

INT_CPU1=$(cat /proc/stat | grep cpu | head -n1)
sleep 1
INT_CPU2=$(cat /proc/stat | grep cpu | head -n1)

CPU_USUARIO1=`valor_USUARIO $INT_CPU1`
CPU_USUARIO2=`valor_USUARIO $INT_CPU2`

CPU_NICE1=`valor_NICE $INT_CPU1`
CPU_NICE2=`valor_NICE $INT_CPU2`

CPU_SISTEMA1=`valor_SISTEMA $INT_CPU1`
CPU_SISTEMA2=`valor_SISTEMA $INT_CPU2`

CPU_IDLE1=`valor_IDLE $INT_CPU1`
CPU_IDLE2=`valor_IDLE $INT_CPU2`

CPU_USUARIO=`expr $CPU_USUARIO2 - $CPU_USUARIO1`
CPU_NICE=`expr $CPU_NICE2 - $CPU_NICE1`
CPU_SISTEMA=`expr $CPU_SISTEMA2 - $CPU_SISTEMA1`
CPU_IDLE=`expr $CPU_IDLE2 - $CPU_IDLE1`

CPU_TOTAL=`expr $CPU_USUARIO + $CPU_SISTEMA + $CPU_NICE`
CPU_MAXIMA=`expr $CPU_TOTAL + $CPU_IDLE`


# RATIO_CPU_USUARIO=`expr $CPU_USUARIO \* 100 / $CPU_MAXIMA`
# RATIO_CPU_SISTEMA=`expr $CPU_SISTEMA \* 100 / $CPU_MAXIMA`
RATIO_CPU_TOTAL=`expr $CPU_TOTAL \* 100 / $CPU_MAXIMA`

echo "$RATIO_CPU_TOTAL"
```

#### Ejemplo de llamada

``` bash
/home/linaro/scripts/var_CPU.sh
```

#### Ejemplo de resultado

```
53
```

### Información del uso de uno de los cores de la CPU:

El nombre usado para el script ha sido `val_CPU_id.sh` y se le pasa un parámetro con el identificador del core.
El identificador de core empieza en 0.

El script realiza 2 lecturas del fichero `/proc/stat` con una diferencia de tiempo de 1 segundo, de esta forma resta las dos lecturas y devuelve el uso de CPU durante el último segundo. La variable que consulta es `cpu?`, siendo `?` el número de core deseado.

#### Contenido del script

``` bash
#!/bin/bash

function valor_USUARIO ()
{
	CPU_AUX=$2
	echo $CPU_AUX
}

function valor_NICE ()
{
	CPU_AUX=$3
	echo $CPU_AUX
}

function valor_SISTEMA ()
{
	CPU_AUX=$4
	echo $CPU_AUX
}

function valor_IDLE ()
{
	CPU_AUX=$5
	echo $CPU_AUX
}

INT_CPU1=$(cat /proc/stat | grep cpu$1)
sleep 1
INT_CPU2=$(cat /proc/stat | grep cpu$1)

CPU_USUARIO1=`valor_USUARIO $INT_CPU1`
CPU_USUARIO2=`valor_USUARIO $INT_CPU2`

CPU_NICE1=`valor_NICE $INT_CPU1`
CPU_NICE2=`valor_NICE $INT_CPU2`

CPU_SISTEMA1=`valor_SISTEMA $INT_CPU1`
CPU_SISTEMA2=`valor_SISTEMA $INT_CPU2`

CPU_IDLE1=`valor_IDLE $INT_CPU1`
CPU_IDLE2=`valor_IDLE $INT_CPU2`

CPU_USUARIO=`expr $CPU_USUARIO2 - $CPU_USUARIO1`
CPU_NICE=`expr $CPU_NICE2 - $CPU_NICE1`
CPU_SISTEMA=`expr $CPU_SISTEMA2 - $CPU_SISTEMA1`
CPU_IDLE=`expr $CPU_IDLE2 - $CPU_IDLE1`

# CPU_USUARIO=$(cat /proc/stat | grep cpu0 | cut -f2 -d " ")
# CPU_NICE=$(cat /proc/stat | grep cpu0 | cut -f3 -d " ")
# CPU_SISTEMA=$(cat /proc/stat | grep cpu0 | cut -f4 -d " ")
# CPU_IDLE=$(cat /proc/stat | grep cpu0 | cut -f5 -d " ")

CPU_TOTAL=`expr $CPU_USUARIO + $CPU_SISTEMA + $CPU_NICE`
CPU_MAXIMA=`expr $CPU_TOTAL + $CPU_IDLE`


# RATIO_CPU_USUARIO=`expr $CPU_USUARIO \* 100 / $CPU_MAXIMA`
# RATIO_CPU_SISTEMA=`expr $CPU_SISTEMA \* 100 / $CPU_MAXIMA`
RATIO_CPU_TOTAL=`expr $CPU_TOTAL \* 100 / $CPU_MAXIMA`

echo $RATIO_CPU_TOTAL
```

#### Ejemplo de llamada

``` bash
/home/linaro/scripts/var_CPU_id.sh 0
```

#### Ejemplo de resultado

```
5
```


## Página web modificada para mostrar la nueva información obtenida

``` php
<?php

echo '<Hr /><H2>CPU</H2>';

echo '<Hr /><h3>Uso CPU</h3> <hr />';
echo '<pre>';
echo 'CPU total: ';
echo exec('/home/linaro/scripts/var_CPU.sh');
echo ' % ';
echo 'CPU 0: ';
echo exec('/home/linaro/scripts/var_CPU_id.sh 0');
echo ' % ';
echo 'CPU 1: ';
echo exec('/home/linaro/scripts/var_CPU_id.sh 1');
echo ' %';
echo '</pre>';

echo '<Hr /><h3>Temperatura CPU</h3><hr />';
echo '<pre>';
$ultima_linea = system('/home/linaro/scripts/temperatura.sh', $retval);
echo '</pre>';

echo '<Hr />';


echo '<br/>';
echo '<br/>';


echo '<Hr /><H2>DISCO DURO</H2>';

echo '<Hr /><h3>Temperatura disco duro</h3><hr />';
echo '<pre>';
$ultima_linea = system('sudo hddtemp /dev/sda', $retval);
echo '</pre>';

echo '<Hr /><h3>Espacio en disco</h3><hr />';
echo '<pre>';
$ultima_linea = system('df -h', $retval);
echo '</pre>';

echo '<Hr /><h3>SMART disco duro</h3><hr />';
echo '<pre>';
$ultima_linea = system('sudo smartctl -A /dev/sda', $retval);
echo '</pre>';

echo '<Hr />';
?>
```
