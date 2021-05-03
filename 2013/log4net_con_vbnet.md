# Log4net con VB.NET

Para poder utilizar el Log4net en una aplicación de VB.NET se han de seguir los siguientes pasos.

Añadir el log4net a las referencias del proyecto.

La inicialización de Log4NET se realiza incluyendo la siguiente llamada en el fichero `AssemblyInfo.vb`:

``` xml
<Assembly: log4net.Config.XmlConfigurator(ConfigFile:="Configuracion.log4net", Watch:=True)>
```


Esta línea hace que se cargue la configuración del Log4net desde el fichero `Configuracion.log4net`.

En la declaración de las variables de las clases añadir:

``` vb
Private ReadOnly LogPagina As log4net.ILog = log4net.LogManager.GetLogger(System.Reflection.MethodBase.GetCurrentMethod().DeclaringType)
```




Por cada salida de log realizar la siguiente llamada:

``` vb
LogPagina.debug(texto_a_sacar_por_log);
LogPagina.info(texto_a_sacar_por_log);
LogPagina.warn(texto_a_sacar_por_log);
LogPagina.error(texto_a_sacar_por_log);
LogPagina.fatal(texto_a_sacar_por_log);
```


Si queremos que en una excepción se imprima el error que contiene el objeto excepción:

``` vb
LogPagina.debug(texto_a_sacar_por_log, excepción);
LogPagina.info(texto_a_sacar_por_log, excepción);
LogPagina.warn(texto_a_sacar_por_log, excepción);
LogPagina.error(texto_a_sacar_por_log, excepción);
LogPagina.fatal(texto_a_sacar_por_log, excepción);
```


El fichero de configuración del Log4Net ha de llamarse `Configuracion.log4net` y ha de estar situado en la raiz del proyecto.

``` xml
<?xml version="1.0" encoding="utf-8" ?>
<log4net>

  <appender name="RollingLogFileAppender" type="log4net.Appender.RollingFileAppender">
    <file value="log\Mtmnet.log" />
    <appendToFile value="true" />
    <rollingStyle value="Size" />
    <maxSizeRollBackups value="10" />
    <maximumFileSize value="10MB" />
    <staticLogFileName value="true" />
    <layout type="log4net.Layout.PatternLayout">
      <conversionPattern value="%d [%t] %-5p %c - %m%n" />
    </layout>
  </appender>

  <root>
    <level value="ALL" />
    <appender-ref ref="RollingLogFileAppender" />
  </root></log4net>
```

