# Reseteo del ID y de la MAC de una máquina virtual en VMware

Para resetear el ID de una máquina virtual se han de borrar las líneas que contengan las siguientes entradas:

```
uuid.location
uuid.bios
```
Para resetear la MAC de la tarjeta de red hay que borrar las siguientes líneas

```
ethernet0.generatedAddress
ethernet0.generatedAddressOffset
```

Además es obligado que esta línea tenga este valor
```
ethernet0.addressType = "generated".
```
