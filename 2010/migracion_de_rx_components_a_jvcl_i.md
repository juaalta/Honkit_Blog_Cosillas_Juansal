# Migración de RX Components a JVCL I

En estas entradas voy a poner los componentes del RX y su equivalente en JVCL.
En este primer artículo sólo voy a poner el *TFormPlacement*.
El equivalente a este en JVCL es *TJvFormStorage*.

Los métodos de ambos son los mismos. El segundo es igual que el primer con más parámetros y métodos, pero los métodos y parámetros del primero estan en el segundo.
La única novedad que hay que señalar es que para que guarde necesitamos un *AppStorage*, los que hay disponibles son:

* TJvAppIniFileStorage
* TJvAppRegistryStorage
* TJvAppDBStorage
* TJvAppXMLFileStorage

Con sólo asignar uno de estos *AppStorage* al *TJvFormStorage* y configurarlo funciona.
