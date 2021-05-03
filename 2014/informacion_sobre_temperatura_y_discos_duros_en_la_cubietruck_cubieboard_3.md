# Información sobre temperatura y discos duros en la cubietruck (cubieboard 3)

## Obtención de la temperatura de la cubietruck:

Se ha de crear un script que contenga el siguiente código:

``` bash
#!/bin/bash
cat /sys/devices/platform/sunxi-i2c.0/i2c-0/0-0034/temp1_input | awk '{ printf ("CPU Temperature = %0.1f°C\n",$1/1000); }'
```

La ejecución del script que se acaba de crear es la siguiente:

    CPU Temperature = 52.2°C



## Información de los discos:

### smartmontools
Para obtener la información de los discos se puede utiliar el paquete smartmontools:

``` bash
apt-get install smartmontools
```

Para obtener la información de la unidad sda1:

``` bash
smartctl -A /dev/sda
```

se obtiene una información similar a:

```
smartctl 5.43 2012-06-30 r3573 [armv7l-linux-3.4.61+] (local build)
Copyright (C) 2002-12 by Bruce Allen, http://smartmontools.sourceforge.net

=== START OF READ SMART DATA SECTION ===
SMART Attributes Data Structure revision number: 16
Vendor Specific SMART Attributes with Thresholds:
ID# ATTRIBUTE_NAME          FLAG     VALUE WORST THRESH TYPE      UPDATED  WHEN_FAILED RAW_VALUE
  1 Raw_Read_Error_Rate     0x002f   200   200   051    Pre-fail  Always       -       0
  3 Spin_Up_Time            0x0027   179   179   021    Pre-fail  Always       -       2016
  4 Start_Stop_Count        0x0032   100   100   000    Old_age   Always       -       299
  5 Reallocated_Sector_Ct   0x0033   200   200   140    Pre-fail  Always       -       0
  7 Seek_Error_Rate         0x002e   200   200   000    Old_age   Always       -       0
  9 Power_On_Hours          0x0032   100   100   000    Old_age   Always       -       253
 10 Spin_Retry_Count        0x0032   100   100   000    Old_age   Always       -       0
 11 Calibration_Retry_Count 0x0032   100   253   000    Old_age   Always       -       0
 12 Power_Cycle_Count       0x0032   100   100   000    Old_age   Always       -       43
191 G-Sense_Error_Rate      0x0032   100   100   000    Old_age   Always       -       0
192 Power-Off_Retract_Count 0x0032   200   200   000    Old_age   Always       -       41
193 Load_Cycle_Count        0x0032   200   200   000    Old_age   Always       -       680
194 Temperature_Celsius     0x0022   092   085   000    Old_age   Always       -       55
196 Reallocated_Event_Count 0x0032   200   200   000    Old_age   Always       -       0
197 Current_Pending_Sector  0x0032   200   200   000    Old_age   Always       -       0
198 Offline_Uncorrectable   0x0030   100   253   000    Old_age   Offline      -       0
199 UDMA_CRC_Error_Count    0x0032   200   200   000    Old_age   Always       -       0
200 Multi_Zone_Error_Rate   0x0008   100   253   000    Old_age   Offline      -       0
```

### hddtemp
Para obtener la información de los discos se puede utilizar el paquete hddtemp:

``` bash
apt-get install hddtemp
```
Cuando pregunte si se quiere dejar como demonio he dicho que no.

Para obtener la información de la temperatura:

``` bash
hddtemp /dev/sda
```

Se obtiene una salida similar a:

    /dev/sda: WDC WD10JPVX-22JC3T0: 55°C




# Información obtenida de:

[Información temperatura y discos duros](http://www.cubieforums.com/index.php/topic,2004.0.html)

[Fstab](https://help.ubuntu.com/community/Fstab)


