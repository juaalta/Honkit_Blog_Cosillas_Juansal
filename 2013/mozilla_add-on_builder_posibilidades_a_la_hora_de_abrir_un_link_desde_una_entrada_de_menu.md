# Mozilla Add-on builder: Posibilidades a la hora de abrir un link desde una entrada de menú

Las posibilidades son las siguientes:

`require("windows").browserWindows.open(pageURL);` abre la url en una ventana nueva.

`require("windows").browserWindows.activewindow.open(pageURL);` abre la url en una pestaña nueva.

`require("tabs").open(pageURL);` abre la url en una pestaña nueva.

`require("tabs").activeTab.url=pageURL;` abre la url en la pestaña actual.


Para el siguiente ejemplo los cambios habría que hacerlos dentro del onMessage:

Fichero: **main.js**

``` javascript
var contextMenu = require("context-menu");
var data = require("self").data;

//Menu contextual para cuando se selecciona un link en la página.
var searchMenu = contextMenu.Menu({
  label: "Abrir URL ",
  context: contextMenu.SelectorContext("a[href]"),
  contentScriptFile: [data.url("links.js")],
  items: [],
  onMessage: function (pageURL) {
    require("tabs").open(pageURL);
  }
});
```



Fichero: **links.js**

``` javascript
self.on("click", function (node, data)
{
    var searchURL = data + node.baseURI;
    self.postMessage(searchURL);
});
```

