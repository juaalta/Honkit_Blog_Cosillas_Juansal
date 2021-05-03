# Instalación y primeros pasos con Haroopress
Como dicen en su github:
```
 A static site generator built with Node.js, "Haroo" means "a day" Support Markdown presentation, Syntax Highlight, Themes
```

Es un generador de páginas web estátias hecho con Node.js.

Su web es: [http://haroopress.com](http://haroopress.com)  
Si github es: [https://github.com/rhiokim/haroopress](https://github.com/rhiokim/haroopress)

Su uso se vuelve un poco complicado al principio, ya que su web y el site por defecto que este crea están en idioma coreano.


## Instalación requisitos previos:

Los requerimientos prévios para la instalación son los siguientes:

### Node.js

``` bash
yum install nodejs
```

### Git

``` bash
yum install git
```

## Instalación

Los pasos que he seguido para la instalación han sido los siguientes:

### Obtención del programa:
Los comandos ejecutados han sido:
``` bash
mkdir haroopress_test
git clone https://github.com/rhiokim/haroopress.git haroopress_test
```

El resultado por pantalla ha sido

```
Cloning into 'haroopress_test'...
remote: Counting objects: 6758, done.
remote: Total 6758 (delta 0), reused 0 (delta 0), pack-reused 6758
Receiving objects: 100% (6758/6758), 22.34 MiB | 941.00 KiB/s, done.
Resolving deltas: 100% (2821/2821), done.
Checking connectivity... done.
```

### Inicialización del sitio web:
Los comandos ejecutados han sido:
``` bash
cd haroopress_test

git config --global user.email "email"
git config --global user.name "username"

sudo make init
```

La ejecución del comando anterior da como resultado la siguiente salida por pantalla, en la cual se nos pide información básica sobre la web a generar.
```
npm install -g node-gyp
npm http GET https://registry.npmjs.org/node-gyp
npm http 304 https://registry.npmjs.org/node-gyp
npm http GET https://registry.npmjs.org/graceful-fs
npm http GET https://registry.npmjs.org/minimatch
npm http GET https://registry.npmjs.org/mkdirp
npm http GET https://registry.npmjs.org/nopt
npm http GET https://registry.npmjs.org/npmlog
npm http GET https://registry.npmjs.org/tar
npm http GET https://registry.npmjs.org/fstream
npm http GET https://registry.npmjs.org/osenv
npm http GET https://registry.npmjs.org/rimraf
npm http GET https://registry.npmjs.org/which
npm http GET https://registry.npmjs.org/request
npm http GET https://registry.npmjs.org/glob
npm http GET https://registry.npmjs.org/semver
npm http 304 https://registry.npmjs.org/graceful-fs
npm http 304 https://registry.npmjs.org/npmlog
npm http 200 https://registry.npmjs.org/mkdirp
npm http 304 https://registry.npmjs.org/tar
npm http 200 https://registry.npmjs.org/nopt
npm http 304 https://registry.npmjs.org/fstream
npm http 304 https://registry.npmjs.org/osenv
npm http 200 https://registry.npmjs.org/minimatch
npm http 304 https://registry.npmjs.org/which
npm http 200 https://registry.npmjs.org/rimraf
npm http 200 https://registry.npmjs.org/semver
npm http 200 https://registry.npmjs.org/glob
npm http GET https://registry.npmjs.org/rimraf/-/rimraf-2.3.3.tgz
npm http GET https://registry.npmjs.org/semver/-/semver-4.3.4.tgz
npm http 200 https://registry.npmjs.org/request
npm http 200 https://registry.npmjs.org/rimraf/-/rimraf-2.3.3.tgz
npm http 200 https://registry.npmjs.org/semver/-/semver-4.3.4.tgz
npm http GET https://registry.npmjs.org/abbrev
npm http GET https://registry.npmjs.org/inflight
npm http GET https://registry.npmjs.org/once
npm http GET https://registry.npmjs.org/inherits
npm http GET https://registry.npmjs.org/minimatch/-/minimatch-2.0.7.tgz
npm http GET https://registry.npmjs.org/gauge
npm http GET https://registry.npmjs.org/ansi
npm http GET https://registry.npmjs.org/are-we-there-yet
npm http GET https://registry.npmjs.org/lru-cache
npm http GET https://registry.npmjs.org/sigmund
npm http GET https://registry.npmjs.org/minimist/0.0.8
npm http 304 https://registry.npmjs.org/abbrev
npm http 200 https://registry.npmjs.org/once
npm http 304 https://registry.npmjs.org/ansi
npm http 200 https://registry.npmjs.org/inflight
npm http 200 https://registry.npmjs.org/inherits
npm http GET https://registry.npmjs.org/inherits
npm http 304 https://registry.npmjs.org/are-we-there-yet
npm http GET https://registry.npmjs.org/once/-/once-1.3.2.tgz
npm http 200 https://registry.npmjs.org/sigmund
npm http 200 https://registry.npmjs.org/minimatch/-/minimatch-2.0.7.tgz
npm http 200 https://registry.npmjs.org/minimist/0.0.8
npm http 304 https://registry.npmjs.org/gauge
npm http 200 https://registry.npmjs.org/inherits
npm http GET https://registry.npmjs.org/minimist/-/minimist-0.0.8.tgz
npm http 200 https://registry.npmjs.org/once/-/once-1.3.2.tgz
npm http GET https://registry.npmjs.org/delegates
npm http 200 https://registry.npmjs.org/minimist/-/minimist-0.0.8.tgz
npm http GET https://registry.npmjs.org/readable-stream
npm http 200 https://registry.npmjs.org/lru-cache
npm http GET https://registry.npmjs.org/block-stream
npm http GET https://registry.npmjs.org/forever-agent
npm http GET https://registry.npmjs.org/form-data
npm http GET https://registry.npmjs.org/json-stringify-safe
npm http GET https://registry.npmjs.org/mime-types
npm http GET https://registry.npmjs.org/node-uuid
npm http GET https://registry.npmjs.org/qs
npm http GET https://registry.npmjs.org/tunnel-agent
npm http GET https://registry.npmjs.org/oauth-sign
npm http GET https://registry.npmjs.org/tough-cookie
npm http GET https://registry.npmjs.org/http-signature
npm http GET https://registry.npmjs.org/aws-sign2
npm http GET https://registry.npmjs.org/hawk
npm http GET https://registry.npmjs.org/stringstream
npm http GET https://registry.npmjs.org/combined-stream
npm http GET https://registry.npmjs.org/isstream
npm http GET https://registry.npmjs.org/har-validator
npm http GET https://registry.npmjs.org/caseless
npm http GET https://registry.npmjs.org/bl
npm http GET https://registry.npmjs.org/lru-cache/-/lru-cache-2.6.2.tgz
npm http GET https://registry.npmjs.org/lodash.pad
npm http GET https://registry.npmjs.org/lodash.padleft
npm http GET https://registry.npmjs.org/lodash.padright
npm http GET https://registry.npmjs.org/has-unicode
npm http 304 https://registry.npmjs.org/delegates
npm http 304 https://registry.npmjs.org/block-stream
npm http 304 https://registry.npmjs.org/json-stringify-safe
npm http GET https://registry.npmjs.org/wrappy
npm http 200 https://registry.npmjs.org/readable-stream
npm http 304 https://registry.npmjs.org/forever-agent
npm http 200 https://registry.npmjs.org/form-data
npm http 200 https://registry.npmjs.org/mime-types
npm http 200 https://registry.npmjs.org/node-uuid
npm http 200 https://registry.npmjs.org/tunnel-agent
npm http 200 https://registry.npmjs.org/lru-cache/-/lru-cache-2.6.2.tgz
npm http 304 https://registry.npmjs.org/oauth-sign
npm http 200 https://registry.npmjs.org/qs
npm http 304 https://registry.npmjs.org/http-signature
npm http 304 https://registry.npmjs.org/aws-sign2
npm http 304 https://registry.npmjs.org/hawk
npm http 304 https://registry.npmjs.org/stringstream
npm http 200 https://registry.npmjs.org/tough-cookie
npm http 200 https://registry.npmjs.org/combined-stream
npm http 304 https://registry.npmjs.org/isstream
npm http 304 https://registry.npmjs.org/caseless
npm http GET https://registry.npmjs.org/mime-types/-/mime-types-2.0.11.tgz
npm http 200 https://registry.npmjs.org/har-validator
npm http 304 https://registry.npmjs.org/lodash.pad
npm http 200 https://registry.npmjs.org/lodash.padright
npm http 200 https://registry.npmjs.org/bl
npm http 304 https://registry.npmjs.org/has-unicode
npm http 200 https://registry.npmjs.org/wrappy
npm http 200 https://registry.npmjs.org/lodash.padleft
npm http GET https://registry.npmjs.org/tough-cookie/-/tough-cookie-1.1.0.tgz
npm http GET https://registry.npmjs.org/har-validator/-/har-validator-1.7.0.tgz
npm http GET https://registry.npmjs.org/lodash.padright/-/lodash.padright-3.1.1.tgz
npm http GET https://registry.npmjs.org/lodash.padleft/-/lodash.padleft-3.1.1.tgz
npm http 200 https://registry.npmjs.org/mime-types/-/mime-types-2.0.11.tgz
npm http GET https://registry.npmjs.org/brace-expansion
npm http 200 https://registry.npmjs.org/har-validator/-/har-validator-1.7.0.tgz
npm http 200 https://registry.npmjs.org/tough-cookie/-/tough-cookie-1.1.0.tgz
npm http 200 https://registry.npmjs.org/lodash.padleft/-/lodash.padleft-3.1.1.tgz
npm http 200 https://registry.npmjs.org/lodash.padright/-/lodash.padright-3.1.1.tgz
npm http 304 https://registry.npmjs.org/brace-expansion
npm http GET https://registry.npmjs.org/string_decoder
npm http GET https://registry.npmjs.org/core-util-is
npm http GET https://registry.npmjs.org/isarray/0.0.1
npm http GET https://registry.npmjs.org/lodash._basetostring
npm http 304 https://registry.npmjs.org/string_decoder
npm http GET https://registry.npmjs.org/lodash._createpadding
npm http 304 https://registry.npmjs.org/core-util-is
npm http 304 https://registry.npmjs.org/isarray/0.0.1
npm http GET https://registry.npmjs.org/balanced-match
npm http GET https://registry.npmjs.org/concat-map/0.0.1
npm http 304 https://registry.npmjs.org/lodash._createpadding
npm http 304 https://registry.npmjs.org/lodash._basetostring
npm http 304 https://registry.npmjs.org/balanced-match
npm http GET https://registry.npmjs.org/lodash.repeat
npm http 304 https://registry.npmjs.org/lodash.repeat
npm http 304 https://registry.npmjs.org/concat-map/0.0.1
npm http GET https://registry.npmjs.org/delayed-stream/0.0.5
npm http GET https://registry.npmjs.org/mime-db
npm http GET https://registry.npmjs.org/async
npm http GET https://registry.npmjs.org/asn1/0.1.11
npm http GET https://registry.npmjs.org/ctype/0.5.3
npm http GET https://registry.npmjs.org/assert-plus
npm http 200 https://registry.npmjs.org/delayed-stream/0.0.5
npm http GET https://registry.npmjs.org/delayed-stream/-/delayed-stream-0.0.5.tgz
npm http 304 https://registry.npmjs.org/assert-plus
npm http GET https://registry.npmjs.org/chalk
npm http GET https://registry.npmjs.org/is-my-json-valid
npm http GET https://registry.npmjs.org/commander
npm http GET https://registry.npmjs.org/bluebird
npm http 200 https://registry.npmjs.org/mime-db
npm http GET https://registry.npmjs.org/mime-db/-/mime-db-1.9.1.tgz
npm http 304 https://registry.npmjs.org/asn1/0.1.11
npm http 304 https://registry.npmjs.org/ctype/0.5.3
npm http 200 https://registry.npmjs.org/is-my-json-valid
npm http 200 https://registry.npmjs.org/async
npm http 200 https://registry.npmjs.org/delayed-stream/-/delayed-stream-0.0.5.tgz
npm http 200 https://registry.npmjs.org/commander
npm http GET https://registry.npmjs.org/commander/-/commander-2.8.1.tgz
npm http 200 https://registry.npmjs.org/chalk
npm http 200 https://registry.npmjs.org/mime-db/-/mime-db-1.9.1.tgz
npm http GET https://registry.npmjs.org/cryptiles
npm http GET https://registry.npmjs.org/sntp
npm http GET https://registry.npmjs.org/boom
npm http GET https://registry.npmjs.org/hoek
npm http 200 https://registry.npmjs.org/bluebird
npm http GET https://registry.npmjs.org/bluebird/-/bluebird-2.9.25.tgz
npm http 200 https://registry.npmjs.org/commander/-/commander-2.8.1.tgz
npm http 200 https://registry.npmjs.org/cryptiles
npm http 200 https://registry.npmjs.org/sntp
npm http 200 https://registry.npmjs.org/bluebird/-/bluebird-2.9.25.tgz
npm http 200 https://registry.npmjs.org/boom
npm http 200 https://registry.npmjs.org/hoek
npm http GET https://registry.npmjs.org/hoek/-/hoek-2.13.0.tgz
npm http 200 https://registry.npmjs.org/hoek/-/hoek-2.13.0.tgz
npm http GET https://registry.npmjs.org/escape-string-regexp
npm http GET https://registry.npmjs.org/ansi-styles
npm http GET https://registry.npmjs.org/has-ansi
npm http GET https://registry.npmjs.org/strip-ansi
npm http GET https://registry.npmjs.org/supports-color
npm http GET https://registry.npmjs.org/graceful-readlink
npm http GET https://registry.npmjs.org/generate-function
npm http GET https://registry.npmjs.org/generate-object-property
npm http GET https://registry.npmjs.org/xtend
npm http GET https://registry.npmjs.org/jsonpointer
npm http 200 https://registry.npmjs.org/escape-string-regexp
npm http 304 https://registry.npmjs.org/ansi-styles
npm http 304 https://registry.npmjs.org/has-ansi
npm http 304 https://registry.npmjs.org/strip-ansi
npm http 304 https://registry.npmjs.org/graceful-readlink
npm http 304 https://registry.npmjs.org/supports-color
npm http 304 https://registry.npmjs.org/generate-object-property
npm http 304 https://registry.npmjs.org/generate-function
npm http 200 https://registry.npmjs.org/xtend
npm http GET https://registry.npmjs.org/ansi-regex
npm http GET https://registry.npmjs.org/ansi-regex
npm http GET https://registry.npmjs.org/get-stdin
npm http 304 https://registry.npmjs.org/jsonpointer
npm http GET https://registry.npmjs.org/is-property
npm http 304 https://registry.npmjs.org/ansi-regex
npm http 304 https://registry.npmjs.org/get-stdin
npm http 304 https://registry.npmjs.org/ansi-regex
npm http 304 https://registry.npmjs.org/is-property
/bin/node-gyp -> /lib/node_modules/node-gyp/bin/node-gyp.js
npm WARN unmet dependency /lib/node_modules/block-stream requires inherits@'~2.0.0' but will load
npm WARN unmet dependency undefined,
npm WARN unmet dependency which is version undefined
npm WARN unmet dependency /lib/node_modules/fstream requires inherits@'~2.0.0' but will load
npm WARN unmet dependency undefined,
npm WARN unmet dependency which is version undefined
npm WARN unmet dependency /lib/node_modules/fstream-ignore requires inherits@'2' but will load
npm WARN unmet dependency undefined,
npm WARN unmet dependency which is version undefined
npm WARN unmet dependency /lib/node_modules/fstream-npm requires inherits@'2' but will load
npm WARN unmet dependency undefined,
npm WARN unmet dependency which is version undefined
npm WARN unmet dependency /lib/node_modules/glob requires inherits@'2' but will load
npm WARN unmet dependency undefined,
npm WARN unmet dependency which is version undefined
npm WARN unmet dependency /lib/node_modules/npmconf requires inherits@'~2.0.0' but will load
npm WARN unmet dependency undefined,
npm WARN unmet dependency which is version undefined
npm WARN unmet dependency /lib/node_modules/tar requires inherits@'2' but will load
npm WARN unmet dependency undefined,
npm WARN unmet dependency which is version undefined
node-gyp@1.0.3 /lib/node_modules/node-gyp
├── which@1.0.9
├── rimraf@2.3.3
├── osenv@0.1.0
├── graceful-fs@3.0.6
├── nopt@3.0.1 (abbrev@1.0.5)
├── fstream@1.0.4 (inherits@2.0.1)
├── semver@4.3.4
├── tar@1.0.3 (inherits@2.0.1, block-stream@0.0.7)
├── mkdirp@0.5.0 (minimist@0.0.8)
├── minimatch@1.0.0 (sigmund@1.0.0, lru-cache@2.6.2)
├── glob@4.5.3 (inherits@2.0.1, once@1.3.2, inflight@1.0.4, minimatch@2.0.7)
├── npmlog@1.2.0 (ansi@0.3.0, are-we-there-yet@1.0.4, gauge@1.2.0)
└── request@2.55.0 (caseless@0.9.0, json-stringify-safe@5.0.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.6.0, tunnel-agent@0.4.0, isstream@0.1.2, node-uuid@1.4.3, qs@2.4.1, bl@0.9.4, form-data@0.2.0, http-signature@0.10.1, tough-cookie@1.1.0, combined-stream@0.0.7, mime-types@2.0.11, hawk@2.3.1, har-validator@1.7.0)
git submodule update --init --recursive
Submodule 'source/themes' (http://github.com/haroopress/haroopress-themes.git) registered for path 'source/themes'
Cloning into 'source/themes'...
remote: Counting objects: 2071, done.
remote: Total 2071 (delta 0), reused 0 (delta 0), pack-reused 2071
Receiving objects: 100% (2071/2071), 20.07 MiB | 247.00 KiB/s, done.
Resolving deltas: 100% (1117/1117), done.
Checking connectivity... done.
Submodule path 'source/themes': checked out '0b858f95bee3b39e48b47192b19ec8a76b103b22'
cd ./node_modules/robotskirt;node-gyp rebuild
gyp info it worked if it ends with ok
gyp info using node-gyp@1.0.3
gyp info using node@0.10.36 | linux | x64
gyp info spawn python
gyp info spawn args [ '/usr/lib/node_modules/node-gyp/gyp/gyp_main.py',
gyp info spawn args   'binding.gyp',
gyp info spawn args   '-f',
gyp info spawn args   'make',
gyp info spawn args   '-I',
gyp info spawn args   '/home/juansal/haroopress/haroopress_test/node_modules/robotskirt/build/config.gypi',
gyp info spawn args   '-I',
gyp info spawn args   '/usr/lib/node_modules/node-gyp/addon.gypi',
gyp info spawn args   '-I',
gyp info spawn args   '/root/.node-gyp/0.10.36/common.gypi',
gyp info spawn args   '-Dlibrary=shared_library',
gyp info spawn args   '-Dvisibility=default',
gyp info spawn args   '-Dnode_root_dir=/root/.node-gyp/0.10.36',
gyp info spawn args   '-Dmodule_root_dir=/home/juansal/haroopress/haroopress_test/node_modules/robotskirt',
gyp info spawn args   '--depth=.',
gyp info spawn args   '--no-parallel',
gyp info spawn args   '--generator-output',
gyp info spawn args   'build',
gyp info spawn args   '-Goutput_dir=.' ]
gyp info spawn make
gyp info spawn args [ 'BUILDTYPE=Release', '-C', 'build' ]
make[1]: se ingresa al directorio `/home/juansal/haroopress/haroopress_test/node_modules/robotskirt/build'
  CC(target) Release/obj.target/sundown/src/autolink.o
  CC(target) Release/obj.target/sundown/src/buffer.o
  CC(target) Release/obj.target/sundown/src/houdini_href_e.o
  CC(target) Release/obj.target/sundown/src/houdini_html_e.o
  CC(target) Release/obj.target/sundown/src/houdini_html_u.o
  CC(target) Release/obj.target/sundown/src/houdini_js_e.o
  CC(target) Release/obj.target/sundown/src/houdini_js_u.o
  CC(target) Release/obj.target/sundown/src/houdini_uri_e.o
  CC(target) Release/obj.target/sundown/src/houdini_uri_u.o
  CC(target) Release/obj.target/sundown/src/houdini_xml_e.o
  CC(target) Release/obj.target/sundown/src/html.o
  CC(target) Release/obj.target/sundown/src/html_smartypants.o
  CC(target) Release/obj.target/sundown/src/markdown.o
  CC(target) Release/obj.target/sundown/src/stack.o
  AR(target) Release/obj.target/sundown.a
  COPY Release/sundown.a
  CXX(target) Release/obj.target/robotskirt/src/robotskirt.o
  SOLINK_MODULE(target) Release/obj.target/robotskirt.node
  SOLINK_MODULE(target) Release/obj.target/robotskirt.node: Finished
  COPY Release/robotskirt.node
make[1]: se sale del directorio `/home/juansal/haroopress/haroopress_test/node_modules/robotskirt/build'
gyp info ok
cd ./node_modules/locally/;npm install
========================================
= configurate haroopress
========================================
./bin/setup.js

haroo> Insert your site title (*) "My Haoopress Blog"
 > Haroopress Test
haroo> Insert your site description (*) "My Development diary, I love node.js & javascript"
 > Test de Haroopress sobre github
haroo> Insert site url (*) "http://www.myblog.com"
 > http://juaalta.github.io
haroo> Insert you full name (*) "Rhio Kim (sync to source/data/authors/Rhio Kim.markdown)"
 > Mi nombre
haroo> Insert you gravatar email address (*) "abc123@gmail.com"
 > correo
haroo> Insert you site meta information (*) "javascript, css3, html5"
 > javascript, css3, html5
http://juaalta.github.io Meta Information
-----------------------------------------------
{
    "version": "0.9.2",
    "defaultTitle": "Haroopress Test",
    "description": "Test de Haroopress sobre github",
    "siteUrl": "http://juaalta.github.io",
    "author": "Juansal",
    "email": "juaalta@gmail.com",
    "keywords": [
        "javascript",
        "css3",
        "html5"
    ]
}
haroo> Save? [y/n] :           y
========================================
= clear public & deployment directories
========================================
./bin/clear.js
haroo> clear to deploy directory¶
haroo> clear to public directory
========================================
= setup repository for deployment
========================================
cd ./bin/;./gh-pages.js
haroo> Enter the read/write repository for your haroopress site
"https://github.com/[github-id]/[github-id].github.io.git"
 >
haroo> git remote -v¶
origin	https://github.com/rhiokim/haroopress.git (fetch)
origin	https://github.com/rhiokim/haroopress.git (push)

haroo> Start setting github pages branch ¶
Initialized empty Git repository in /home/juansal/haroopress/haroopress_test/_deploy/.git/

haroo> Completed git repository initialize ¶

haroo> Repository remote's name origin -> haroopress ¶
haroo> Git remote add to origin ¶

haroo> Added remote https://github.com/juaalta/juaalta.github.io.git as origin ¶

haroo> Set origin as default remote ¶

haroo> Created inex.html ¶

haroo> git add . ¶

haroo> Copy temp commiter ¶

haroo> git commit ¶

haroo> Remove temp commiter ¶

haroo> git remote add origin ¶
========================================
= create default data set
========================================
./bin/init.js
haroo> created initial data
haroo> site data initialized
clear
[3;J
cat ./lib/haroopress/QUICK.markdown
# Quick guide
\`\`\`
$ make gen       // 정적 페이지 생성
$ make preview   // 미리보기
$ make new-post  // 새로운 글 작성
$ make new-page  // 새로운 페이지 작성
$ make new-slide // 새로운 웹 슬라이드 작성
\`\`\`
# Read more
* 하루프레스 공식 : http://haroopress.com
* 새로운 포스트 작성 : http://haroopress.com/post/haroopress-posting-guide/
* 블로그 퍼블리싱 : http://haroopress.com/post/haroopress-deploy-to-github/

Copyright © haroopress / Contact to rhio.kim@gmail.com
Source http://github.com/rhiokim/haroopress
Issue https://github.com/rhiokim/haroopress/issues
```

Si el comando anterior no se ejecuta con sudo delante se obtiene el siguiente error:
```
npm install -g node-gyp
npm http GET https://registry.npmjs.org/node-gyp
npm http 304 https://registry.npmjs.org/node-gyp
npm ERR! error rolling back Error: EACCES, unlink '/bin/node-gyp'
npm ERR! error rolling back  node-gyp@1.0.3 { [Error: EACCES, unlink '/bin/node-gyp'] errno: 3, code: 'EACCES', path: '/bin/node-gyp' }
npm ERR! Error: EACCES, unlink '/bin/node-gyp'
npm ERR!  { [Error: EACCES, unlink '/bin/node-gyp'] errno: 3, code: 'EACCES', path: '/bin/node-gyp' }
npm ERR!
npm ERR! Please try running this command again as root/Administrator.

npm ERR! System Linux 3.19.4-100.fc20.x86_64
npm ERR! command "node" "/bin/npm" "install" "-g" "node-gyp"
npm ERR! cwd /home/juansal/haroopress/haroopress_test
npm ERR! node -v v0.10.36
npm ERR! npm -v 1.3.6
npm ERR! path /bin/node-gyp
npm ERR! code EACCES
npm ERR! errno 3
npm ERR! stack Error: EACCES, unlink '/bin/node-gyp'
npm ERR!
npm ERR! Additional logging details can be found in:
npm ERR!     /home/juansal/haroopress/haroopress_test/npm-debug.log
npm ERR! not ok code 0
make: *** [initialize] Error 3
```

## Uso de haroopress

### Comandos de previsualización y publicación

#### Establecer el repositorio GitHub para desplegar la web
Este comando no es preciso lanzarlo, si en el paso anterior ha sido configurado el repositorio de github.
``` bash
make gh-pages
```

La ejecución de este comando da como resultado:
```
========================================
= clear public & deployment directories
========================================
./bin/clear.js
haroo> clear to deploy directory¶
haroo> clear to public directory
========================================
= setup repository for deployment
========================================
cd ./bin/;./gh-pages.js
haroo> Enter the read/write repository for your haroopress site
"https://github.com/[github-id]/[github-id].github.io.git"
 > https://github.com/juaalta/juaalta.github.io.git
haroo> git remote -v¶
origin	https://github.com/juaalta/juaalta.github.io.git (fetch)
origin	https://github.com/juaalta/juaalta.github.io.git (push)
```
Durante la ejecución del comando se nos pide la ruta de github en la que se subirá el repositorio.

#### Generar las páginas estáticas
``` bash
make gen
```

La ejecución de este comando da como resultado:
```
========================================
= clear public & deployment directories
========================================
./bin/clear.js
haroo> clear to deploy directory¶
haroo> clear to public directory
========================================
= generate to static page
========================================
./bin/gen.js
haroo> cp -R /home/juansal/haroopress/haroopress_test/source/themes/basic/public/* /home/juansal/haroopress/haroopress_test/_public
haroo> export rss.xml ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/rss.xml
haroo> export 404.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/404.html
haroo> export index.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/index.html
haroo> export archives.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/archives/index.html
haroo> export article.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/post/welcome-to-haroopress/index.html
haroo> /home/juansal/haroopress/haroopress_test/_public/post/presentacion/index.html
haroo> export slides ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/slides/hello-world/index.html
haroo> export slides.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/slides/index.html
haroo> export categories.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/category/index.html
haroo> export category.html ¶
haroo> export authors.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/authors/index.html
haroo> export author.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/authors/Juansal/index.html
haroo> /home/juansal/haroopress/haroopress_test/_public/authors/haroopress/index.html
haroo> export pages.html ¶
=====================================
==       content statistics        ==
=====================================
== article | publish(2) | draft(1) ==
== page    | publish(0) | draft(1) ==
== slide   | publish(1) | draft(0) ==
=====================================
mkdir -p ./_public/slides/@asserts
cp -R ./lib/shower/themes ./_public/slides/@asserts
cp -R ./lib/shower/scripts ./_public/slides/@asserts
cp -R ./lib/bootstrap/* ./_public
```

#### Previsualizar en local la web generada
``` bash
make preview
```

La ejecución de este comando da como resultado:
```
========================================
= clear public & deployment directories
========================================
./bin/clear.js
haroo> clear to deploy directory¶
haroo> clear to public directory
========================================
= generate to static page
========================================
./bin/gen.js
haroo> cp -R /home/juansal/haroopress/haroopress_test/source/themes/basic/public/* /home/juansal/haroopress/haroopress_test/_public
haroo> export rss.xml ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/rss.xml
haroo> export 404.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/404.html
haroo> export index.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/index.html
haroo> export archives.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/archives/index.html
haroo> export article.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/post/welcome-to-haroopress/index.html
haroo> /home/juansal/haroopress/haroopress_test/_public/post/presentacion/index.html
haroo> export slides ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/slides/hello-world/index.html
haroo> export slides.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/slides/index.html
haroo> export categories.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/category/index.html
haroo> export category.html ¶
haroo> export authors.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/authors/index.html
haroo> export author.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/authors/Juansal/index.html
haroo> /home/juansal/haroopress/haroopress_test/_public/authors/haroopress/index.html
haroo> export pages.html ¶
=====================================
==       content statistics        ==
=====================================
== article | publish(2) | draft(1) ==
== page    | publish(0) | draft(1) ==
== slide   | publish(1) | draft(0) ==
=====================================
mkdir -p ./_public/slides/@asserts
cp -R ./lib/shower/themes ./_public/slides/@asserts
cp -R ./lib/shower/scripts ./_public/slides/@asserts
cp -R ./lib/bootstrap/* ./_public
========================================
= preview static page
========================================
./bin/preview.js
haroo> Start server at http://localhost:8081 ¶
Do you want check on the browser? [y(es)/n] : n
haroo> You can check your site on the web browser. ( Stop server : ^C )
```
Para finalizar la previsualización se ha de pulsar `ctrl`+`c`

#### Pulicar la web en github
``` bash
make deploy
```

La ejecución de este comando da como resultado:
```
lear public & deployment directories
========================================
./bin/clear.js
haroo> clear to deploy directory¶
haroo> clear to public directory
========================================
= generate to static page
========================================
./bin/gen.js
haroo> cp -R /home/juansal/haroopress/haroopress_test/source/themes/basic/public/* /home/juansal/haroopress/haroopress_test/_public
haroo> export rss.xml ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/rss.xml
haroo> export 404.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/404.html
haroo> export index.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/index.html
haroo> export archives.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/archives/index.html
haroo> export article.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/post/welcome-to-haroopress/index.html
haroo> /home/juansal/haroopress/haroopress_test/_public/post/presentacion/index.html
haroo> export slides ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/slides/hello-world/index.html
haroo> export slides.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/slides/index.html
haroo> export categories.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/category/index.html
haroo> export category.html ¶
haroo> export authors.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/authors/index.html
haroo> export author.html ¶
haroo> /home/juansal/haroopress/haroopress_test/_public/authors/Juansal/index.html
haroo> /home/juansal/haroopress/haroopress_test/_public/authors/haroopress/index.html
haroo> export pages.html ¶
=====================================
==       content statistics        ==
=====================================
== article | publish(2) | draft(1) ==
== page    | publish(0) | draft(1) ==
== slide   | publish(1) | draft(0) ==
=====================================
mkdir -p ./_public/slides/@asserts
cp -R ./lib/shower/themes ./_public/slides/@asserts
cp -R ./lib/shower/scripts ./_public/slides/@asserts
cp -R ./lib/bootstrap/* ./_public
========================================
= deploy to github
========================================
cd ./bin;./deploy.js ""
haroo> Resources copy to Deploy directory
haroo> git add .¶

haroo> git add -u¶

haroo> git commit -m ¶
[master c75a4b7] Site updated at Fri May 08 2015 01:21:18 GMT+0200 (CEST)
 1 file changed, 1 insertion(+), 1 deletion(-)

haroo> git push origin master --force¶

haroo> completed http://juaalta.github.io
haroo> open http://juaalta.github.io ? [y/n]          y
```

### Comandos de generación de contenido

#### Crear un artículo
``` bash
make new-post
```

La ejecución del comando da como resultado:
```
cd ./bin;./new-post.js
haroo> Input article title : Prueva 1
haroo> Input article category : test
haroo> Input article tag (e.g tag1, tag2, tag3) : test
haroo> write post -> /home/juansal/haroopress/haroopress_test/source/data/articles/prueva-1/index.markdown
haroo> article's image path /home/juansal/haroopress/haroopress_test/source/data/articles/prueva-1/@img
```

Para modificar el artículo se ha de modificar el fichero que se indica en la línea `write post ->`, en nuestro caso es `/home/juansal/haroopress/haroopress_test/source/data/articles/prueva-1/index.markdown`.

Las imágenes a añadir al artículo han de guardarse dentro de la carpeta que se indica en la línea `article's image path`, en nuestro caso es `/home/juansal/haroopress/haroopress_test/source/data/articles/prueva-1/@img`.

El contenido de un artículo vacío es:
```
{
    "title": "Prueva 1",
    "author": "Juansal",
    "date": "2015-05-07T23:06:28.322Z",
    "categories": [
        "test"
    ],
    "tags": [
        "test"
    ],
    "acceptComment": true,
    "acceptTrackback": true,
    "published": "2015-05-07T23:06:28.322Z",
    "status": "draft",
    "important": false,
    "advanced": {}
}

write here!
```
Nuestro artículo en Markdown ha de empezar en la línea en la que se encuentra la frase `write here!` (esta frase puede ser borrada, sólo indica el inicio del código del artículo). La información anterior a esta frase es usada por Haroopres.

**Nota importante:**
Mientras la variable `status` contenga el valor **draft**, este artículo no se publicará. Para que se publique se ha de cambiar el valor a **publish**.

#### Crear una página
``` bash
make new-page
```

La ejecución del comando da como resultado:
```
cd ./bin;./new-page.js
haroo> Enter page title : Pagina test 1
haroo> Enter page category (e.g cate1, cate2, cate3 ) : test
haroo> Enter page tag (e.g tag1, tag2, tag3) : test
haroo> created -> /home/juansal/haroopress/haroopress_test/source/data/pages/pagina-test-1/index.markdown
haroo> page's image path /home/juansal/haroopress/haroopress_test/source/data/pages/pagina-test-1/@img
```

Para modificar la página se ha de modificar el fichero que se indica en la línea `created ->`, en nuestro caso es `/home/juansal/haroopress/haroopress_test/source/data/pages/pagina-test-1/index.markdown`.

Las imágenes a añadir a la página han de guardarse dentro de la carpeta que se indica en la línea `page's image path`, en nuestro caso es `/home/juansal/haroopress/haroopress_test/source/data/pages/pagina-test-1/@img`.

El contenido de una página vacía es:
```
{
    "title": "Pagina test 1",
    "author": "Juansal",
    "date": "2015-05-07T23:28:10.571Z",
    "categories": [
        "test"
    ],
    "tags": [
        "test"
    ],
    "acceptComment": true,
    "acceptTrackback": true,
    "published": "2015-05-07T23:28:10.571Z",
    "status": "publish",
    "important": false,
    "advanced": {
        "layout": "",
        "display": ""
    }
}

content here!
```

Nuestro contenido de la página en Markdown ha de empezar en la línea en la que se encuentra la frase `content here!` (esta frase puede ser borrada, sólo indica el inicio del código del artículo). La información anterior a esta frase es usada por Haroopres.

**Nota importante:**
Mientras la variable `status` contenga el valor **draft**, este artículo no se publicará. Para que se publique se ha de cambiar el valor a **publish**.


#### Crear un pase de diapositivas
``` bash
make new-slide
```

La ejecución del comando da como resultado:
```
cd ./bin;./new-slide.js
haroo> Input slide title : Slide Test 1
haroo> Input slide category : test
haroo> Input slide tag (e.g tag1, tag2, tag3) : test
haroo> write slide -> /home/juansal/haroopress/haroopress_test/source/data/slides/slide-test-1/index.markdown
haroo> slide's image path /home/juansal/haroopress/haroopress_test/source/data/slides/slide-test-1/@img

```

Para modificar la presentación se ha de modificar el fichero que se indica en la línea `write slide ->`, en nuestro caso es `/home/juansal/haroopress/haroopress_test/source/data/slides/slide-test-1/index.markdown`.

Las imágenes a añadir a la presentación han de guardarse dentro de la carpeta que se indica en la línea `slide's image path`, en nuestro caso es `/home/juansal/haroopress/haroopress_test/source/data/slides/slide-test-1/@img`.

El contenido de una presentación vacía es:
```
{
    "title": "Slide Test 1",
    "author": "Juansal",
    "date": "2015-05-07T23:32:29.627Z",
    "categories": [
        "test"
    ],
    "tags": [
        "test"
    ],
    "acceptComment": true,
    "acceptTrackback": true,
    "published": "2015-05-07T23:32:29.627Z",
    "status": "draft",
    "important": false,
    "advanced": {
        "layout": "slide",
        "displayCover": true
    }
}

## First Slide

Slide Content Here

Slide Seperator is five hypen (=)

![cover](../_asserts/pictures/cover.jpg)

=====

## Second Slide Title

Slide Content Here


=====

## Third Slide Title

* ul
    - li
    - li
* ul
    - li

=====

## Forth Slide Title

` ` `
var foo = 'bar';
//code here
` ` `

```

Nuestro contenido de la presentación en Markdown ha de empezar en la línea en la que se encuentra la frase `## First Slide` (esta frase puede ser borrada, sólo indica el inicio del código del artículo). La información anterior a esta frase es usada por Haroopres.

**Nota importante:**
Mientras la variable `status` contenga el valor **draft**, este artículo no se publicará. Para que se publique se ha de cambiar el valor a **publish**.

