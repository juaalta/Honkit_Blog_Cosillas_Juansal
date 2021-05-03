# Formato de datos de Haroopress

## Estructura básica de los ficheros de autores y contenido

Los ficheros de autores y contenido (Artículos, Páginas y Presentaciones) estan compuestos por una cabecera en JSON y un contenido en Markdown.

La estructura básica del fichero es:

``` json
{
   Encabezamiento, es fijo por tipo de fichero.
}

Contenido en formato Markdown.
```

Todas las fechas de los encabezados están en formato UTC.

## Organización de directorios y ficheros

### Categorías

Los artículos sin categoría se muestran como Home.
Una categoría es visible si hay algún artículo publicado de ella.
Las categorías se calculan a partir de la información de los títulos.

### Autores

Se encuentran en el directorio `./source/data/authors`. Hay un fichero con mobre `{autor}.markdown`, por cada uno de los autores que se dese visualizar.
Para borrar un autor primero se han de borrar todos los elementos que estén relacionados con el.

#### Estructura del fichero
La estructura del fichero es la siguiente:

``` json
{
    "name": "Nombre del autor, no se puede tocar, si se hace no genera la web",
    "company": "Nombre de la empresa",
    "blog": "Dirección del blog",
    "twitter": "Usuario de twitter",
    "github": "Usuario de github",
    "vimeo": "Usuario de vimeo",
    "youtube": "Usuario de youtube",
    "facebook": "Usuario de facebook",
    "linkedin": "Usuario de linkedin",
    "email": "Dirección de correo que usó para registrarse en gravatar."
}

Texto libre sobre el autor.
```

En estos momentos sólo es visible el nombre, el usuario de twitter y el icono de gravatar.

### Artículos

Se encuentran en el directorio `./source/data/articles`.
Por cada artículo que se crea, se crea un directorio con el nombre de este.
Dentro de este directorio se encuentran los siguientes elementos:
* Directorio **@img**, que contendrá las imágenes.
* Fichero **index.markdown**, que contendrá el contenido del artículo.

#### Estructura del fichero

La estructura del fichero es la siguiente:

``` json
{
    "title": "Titulo de artículo",
    "author": "Autor del artículo",
    "date": "Fecha de creación en formato UTC",
    "categories": [
        "Categorías separadas por comas"
    ],
    "tags": [ "Etiquetas separadas por comas" ],
    "acceptComment": true,                 //Si el artículo permite comentarios (se usa disqus)
    "acceptTrackback": true,               //Si se permite el rastreo.
    "published": "Fecha de publicación en formato UTC",
    "status": "Estado de publicación", //Puede ser: publish o draft.
    "important": false,                         //Si el artículo ha de marcarse como importante.
    "advanced": {}                              //Datos avanzados, en este caso no hay.
}

Texto del artículo.
```

### Páginas

Se encuentran en el directorio `./source/data/pages`.
Por cada página que se crea, se crea un directorio con el nombre de esta.  
Dentro de este directorio se encuentran los siguientes elementos:

* Directorio **@img**, que contendrá las imágenes.
* Fichero **index.markdown**, que contendrá el contenido de la página.

#### Estructura del fichero

La estructura del fichero es la siguiente:

``` json
{
    "title": "Titulo de la página",
    "author": "Autor de la página",
    "date": "Fecha de creación en formato UTC",
    "categories": [
        "Categorías separadas por comas"
    ],
    "tags": [ "Etiquetas separadas por comas" ],
    "acceptComment": true,                 //Si la página permite comentarios (se usa disqus)
    "acceptTrackback": true,               //Si se permite el rastreo.
    "published": "Fecha de publicación en formato UTC",
    "status": "Estado de publicación", //Puede ser: publish o draft.
    "important": false,                         //Si la página ha de marcarse como importante.
    "advanced": {                              //Datos avanzados.
        "layout": "page",
        "display": ""
    }

}

Texto de la página.
```

### Presentaciones

Se encuentran en el directorio `./source/data/slides`.
Por cada presentación que se crea, se crea un directorio con el nombre de esta.
Dentro de este directorio se encuentran los siguientes elementos:

* Directorio **@img**, que contendrá las imágenes.
* Fichero **index.markdown**, que contendrá el contenido de la presentación.

#### Estructura del fichero

La estructura del fichero es la siguiente:

``` json
{
    "title": "Titulo de la presentación",
    "author": "Autor de la presentación",
    "date": "Fecha de creación en formato UTC",
    "categories": [
        "Categorías separadas por comas"
    ],
    "tags": [ "Etiquetas separadas por comas" ],
    "acceptComment": true,                 //Si la presentación permite comentarios (se usa disqus)
    "acceptTrackback": true,               //Si se permite el rastreo.
    "published": "Fecha de publicación en formato UTC",
    "status": "Estado de publicación", //Puede ser: publish o draft.
    "important": false,                         //Si la presentación ha de marcarse como importante.
    "advanced": {                              //Datos avanzados.
         "layout": "slide",
        "displayCover": true
    }

}

Texto de la presentación.
```

### Favoritos

El apartado de favoritos de la web se encuentra en el fichero ./source/data/favorites.markdown

El fichero consiste en una lista de links en formato markdown.
Contenido del fichero original:

```
[하루프레스 공식 사이트](http://haroopress.github.com)
[하루프레스 소스 저장소](http://github.com/rhiokim/haroopress/)
[하루프레스 테마 저장소](http://github.com/haroopress/haroopress-theme)
[하루프레스 개발자 블로그](http://rhio.tistory.com)
[노드 한국 개발자 커뮤니티](http://nodejs.kr)
[프론트 앤드 개발자 커뮤니티](http://frends.kr)
```

### Temas

Se encuentran en el directorio `./source/themes`.
Cada tema corresponde a un directorio y dentro de este directorio están los ficheros que componen el tema.

### Configuración

La configuración básica de Haroopres se encuentra en el fichero `config.js`, este se encuentra en la carpeta raíz de nuestra instancia local de Haroopress.  
Es un fichero en formato JSON.  
Los datos que se pueden configurar son:

* Datos básicos de la web como: nombre, descripción, autor, etc.
* Tema
* Plugins

Ejemplo de fichero:

``` json
module.exports = {
    "meta": {
        "version": "0.9.2",
        "defaultTitle": "Test de Haroopress sobre github",
        "description": "Test de Haroopress sobre github",
        "siteUrl": "http://juaalta.github.io",
        "author": "Juansal",
        "email": "juaalta@gmail.com",
        "keywords": [
            "StaticWebsite",
            "test",
            "haroopress",
            "github"
        ]
    },
    "lang": "es",
    "contentLength": 5,
    "pagenate": 5,
    "dateFormate": "mm:ssa, Do MMM YYYY",
    "deployBranch": "gh-pages",
    "CNAME": "",
    "sourceDir": __dirname +"/source/data",
    "themeDir": __dirname +"/source/themes",
    "publicDir": __dirname +"/_public",
    "deployDir": __dirname +"/_deploy",
    "defaultPort": 8081,
    "defaultSlideStyle": "basic",
    "defaultCodeStyle": "default",
    "theme": {
        "name": "basic"
    },
    "recents": {
        "display": true,
        "articleCount": 5,
        "showNameTag": true
    },
    "analytics": {
        "display": false,
        "googleAnalyticsId": ""
    },
    "plugins": {
        "github": {
            "display": false,
            "user": "",
            "repoCount": 10,
            "skipForks": true
        },
        "tweets": {
            "display": false,
            "user": "",
            "tweetCount": 10
        },
        "twitter": {
            "display": false,
            "user": "",
            "tweetButton": false
        },
        "facebook": {
            "display": false,
            "user": "",
            "showLikeButton": false
        },
        "google": {
            "display": false,
           "googlePlusSize": "medium"
        },
        "disqus": {
            "display": false,
            "shortName": "",
            "showCommentCount": true
        },
        "delicious": {},
        "contributors": {
            "display": true,
            "sort": "DESC",
            "count": 5
        },
        "weather": {
            "display": false,
            "delay": 0,
            "zipcode": "KSXX0037"
        }
    }
}
```
