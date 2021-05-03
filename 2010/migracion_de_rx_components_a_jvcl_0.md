# Migración de RX Components a JVCL 0

Este post deberia de haber aparecido antes del actual, pero por despiste no lo hice y por tanto lo he etiquetado como 0 y no como II.
Para realizar la migración, esta se puede hacer de forma automática. Esto ser realiza mediante una aplicación que tiene JVCL llamada *JVCLConvert*, esta se encuentra en la ruta: `jvcl\devtools\JVCLConvert`.

Para poder realizar la conversión de componentes de forma correcta hay que utilizar plantillas, estas se encuentran en `jvcl\converter` y las que nos interesan son las siguientes:

* RxToJVCLApp.dat
* JVCL3.dat

La primera sirve para realizar la conversión de nombres de clases y la segunda sirve para pasar los nombres de clases de cualquier versión anterior de JVCL a la actual.
Hay que indicar que aunque la segunda no es obligatoria, si que es aconsejable, ya que la plantilla primera podría tener nombres de clases antiguas de JVCL y por tanto la segunda se encarga de actualizar estos nombres.

Otra cosa que no indica la documentación y que si que es recomendable es que una vez transformado el proyecto lo abramos y abramos todos sus formularios ya que puede darse el caso, y a mí se me ha dado, que algún **USES** se haya quedado sin incluir, ya que esta aplicación cambia nombres, pero no añade y puede que alguna clase no tenga incluido su **USES**.
