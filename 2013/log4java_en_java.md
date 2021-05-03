# Log4Java en Java

Para poder utilizar el Log4Java en una aplicación de Java se han de seguir los siguientes pasos.

Añadir los siguientes imports a los ficheros que vayan a utilizarlo.

``` java
import org.apache.log4j.Logger;
```



Al principio de la aplicación hay que introducir esta línea:

``` java
PropertyConfigurator.configure("log4j.properties");
```


Al principio de la clase se ha de introducir la siguiente línea:

``` java
private final Logger logger = Logger.getLogger(this.getClass().getName());
```


Por cada salida a log que queramos obtener tenemos que introducir una de las siguientes líneas de código, dependiendo del nivel de log deseado:

``` java
logger.debug(texto_a_sacar_por_log);
logger.error(texto_a_sacar_por_log);
logger.fatal(texto_a_sacar_por_log);
logger.info(texto_a_sacar_por_log);
```



Si además queremos que saque la información de una excepción obtenida:

``` java
logger.debug(texto_a_sacar_por_log, excepción);
logger.error(texto_a_sacar_por_log, excepción);
logger.fatal(texto_a_sacar_por_log, excepción);
logger.info(texto_a_sacar_por_log, excepción);
```


Ejemplo de un fichero de configuración, esta vez en vez de utilizar un fichero xml utilizaré un fichero properties, en nuestro caso llamado `log4j.properties`:

```
# Registro de los appenders, junto al nivel de log.

log4j.rootLogger=ALL, FLOG


# Appender de fichero circular (RollingFileAppender)
log4j.appender.FLOG=org.apache.log4j.RollingFileAppender
log4j.appender.FLOG.File=log/fingerreader2.log

# Configuración del formato del contenido del fichero de log.
log4j.appender.FLOG.layout=org.apache.log4j.PatternLayout
log4j.appender.FLOG.layout.ConversionPattern=%d [%t] %-5p %c - %m%n

# Configuración del tama\u00f1o del fichero y del número de ficheros
log4j.appender.FLOG.MaxFileSize=10240KB
log4j.appender.FLOG.MaxBackupIndex=10
```


