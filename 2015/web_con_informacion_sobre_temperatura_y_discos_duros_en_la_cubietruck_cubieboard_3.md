# Web con información sobre temperatura y discos duros en la cubietruck (cubieboard 3)

## Finalidad del artículo

La finalidad de este artículo aprovechar los datos obtenidos a partir del [anterior artículo sobre la cubietruck](../2014/informacion_sobre_temperatura_y_discos_duros_en_la_cubietruck_cubieboard_3.md) y mostrar los datos de forma fácil desde una página web.

## Software instalado

Para poder hacer que la cubietruck muestre la web que se desea se ha de instalar el apache y el php.

### Apache

Para instalar el servidor apache se ha de lanzar el siguiente comando:
``` bash
apt-get install apache2
```

### PHP

Para instalar el php se ha de lanzar el siguiente comando:

``` bash
apt-get install php5
```

## Creación de la web:

La web que se ha creado aprovecha los comandos que se comentaron en el artículo anterior sobre [monitorización de temperatura y discos duros de la cubietruck](../2014/informacion_sobre_temperatura_y_discos_duros_en_la_cubietruck_cubieboard_3.md).
Los pasos seguidos han sido los siguientes:

* Se cambia el nombre del fichero `/var/www/index.html` por `/var/www/_index.html` para evitar que cuando nos conectemos lo arranque sin indicar página muestre la por defecto de apache.
* Se crea el fichero `/var/www/index.php`, para que arranque por defecto, cuyo contenido es:

``` php
<?php

echo '<Hr />Espacio en disco <hr />';
echo '<pre>';

// Muestra el resultado completo del comando "df -h", y devuelve la
// ultima linea de la salida en $ultima_linea. Almacena el valor de
// retorno del comando en $retval.
$ultima_linea = system('df -h', $retval);

echo '</pre>';

echo '<Hr />Temperatura CPU<hr />';
echo '<pre>';

$ultima_linea = system('/home/linaro/scripts/temperatura.sh', $retval);

echo '</pre>';

echo '<Hr />Temperatura disco duro<hr />';
echo '<pre>';

$ultima_linea = system('sudo hddtemp /dev/sda', $retval);

echo '</pre>';

echo '<Hr />SMART disco duro<hr />';
echo '<pre>';

$ultima_linea = system('sudo smartctl -A /dev/sda', $retval);

echo '</pre>';


?>

```

El resultado de la consulta de la web (en mi caso http://192.168.0.20) ha sido:

```
--------------------------------------------------------------------------------------------------
Espacio en disco
--------------------------------------------------------------------------------------------------
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        29G  1.6G   26G   6% /
devtmpfs        913M  4.0K  913M   1% /dev
tmpfs            20M  4.0K   20M   1% /tmp
none            183M  188K  183M   1% /run
none            5.0M     0  5.0M   0% /run/lock
none            913M     0  913M   0% /run/shm
none            100M   12K  100M   1% /run/user
/dev/sda1       917G   22G  850G   3% /media/hdd
--------------------------------------------------------------------------------------------------
Temperatura CPU
--------------------------------------------------------------------------------------------------
CPU Temperature = 53.8Â°C
--------------------------------------------------------------------------------------------------
Temperatura disco duro
--------------------------------------------------------------------------------------------------
/dev/sda: WDC WD10JPVX-22JC3T0: 54 C
--------------------------------------------------------------------------------------------------
SMART disco duro
--------------------------------------------------------------------------------------------------
smartctl 5.43 2012-06-30 r3573 [armv7l-linux-3.4.61+] (local build)
Copyright (C) 2002-12 by Bruce Allen, http://smartmontools.sourceforge.net

=== START OF READ SMART DATA SECTION ===
SMART Attributes Data Structure revision number: 16
Vendor Specific SMART Attributes with Thresholds:
ID# ATTRIBUTE_NAME          FLAG     VALUE WORST THRESH TYPE      UPDATED  WHEN_FAILED RAW_VALUE
  1 Raw_Read_Error_Rate     0x002f   200   200   051    Pre-fail  Always       -       0
  3 Spin_Up_Time            0x0027   187   178   021    Pre-fail  Always       -       1608
  4 Start_Stop_Count        0x0032   063   063   000    Old_age   Always       -       37910
  5 Reallocated_Sector_Ct   0x0033   200   200   140    Pre-fail  Always       -       0
  7 Seek_Error_Rate         0x002e   200   200   000    Old_age   Always       -       0
  9 Power_On_Hours          0x0032   097   097   000    Old_age   Always       -       2257
 10 Spin_Retry_Count        0x0032   100   100   000    Old_age   Always       -       0
 11 Calibration_Retry_Count 0x0032   100   100   000    Old_age   Always       -       0
 12 Power_Cycle_Count       0x0032   100   100   000    Old_age   Always       -       220
191 G-Sense_Error_Rate      0x0032   099   099   000    Old_age   Always       -       1
192 Power-Off_Retract_Count 0x0032   200   200   000    Old_age   Always       -       218
193 Load_Cycle_Count        0x0032   178   178   000    Old_age   Always       -       66334
194 Temperature_Celsius     0x0022   093   085   000    Old_age   Always       -       54
196 Reallocated_Event_Count 0x0032   200   200   000    Old_age   Always       -       0
197 Current_Pending_Sector  0x0032   200   200   000    Old_age   Always       -       0
198 Offline_Uncorrectable   0x0030   100   253   000    Old_age   Offline      -       0
199 UDMA_CRC_Error_Count    0x0032   200   200   000    Old_age   Always       -       0
200 Multi_Zone_Error_Rate   0x0008   100   253   000    Old_age   Offline      -       0


```

