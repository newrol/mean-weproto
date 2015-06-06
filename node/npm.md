##NPM


Es un gestor de paquetes de javascript, el cual fue sido adoptado por defecto por node.js a partir de la versión 0.6.3. La compañía que mantiene el proyecto npm es npm.inc, ellos gestionan el cliente y todo el respositorio poniendo a disposición del público tanto repositorios públicos como respositorios open source.

Al utilizar npm para añadir un módulo a nuestra aplicación lo que estamos haciendo es importar una libraría de una versión determinada hacia nuestra aplicación para poder usarla de forma local, este sistema de gestionar módulos es muy parecido al que utiliza maven o gradle para maneter proyectos java.

Así mismo en node.js un módulo puede depender de otros, npm se encargará de mantener la coherencia entre dependencias.

La jerarquía de directorios de un módulo en node.js sería la siguiente:

```javascript
    Nombre del módulo
 \
  |- lib/
      \
       |- PROJECTNAME.js
  |- bin/
      \
       |- BINFILE
  |- examples/
  |- test/
  |- index.js
  |- package.json
  |- README.md

```


 bin: Es la que contendrá las funciones con las que se podrá ejecutar nuestro módulo en la línea de comandos.

 source: Es la que contiene nuestro código fuente.

dist: Es la que contiene el  código Javascript final del módulo.

test: Es la que contiene el código Javascript final de las pruebas unitarias que tenga el módulo.

 .npmignore: Este archivo es necesario para que NPM sepa que archivos de nuestro repositorio ignorar al instalar y descargar nuestro módulo en una máquina cliente.

package.json: Este archivo es necesario para que NPM sepa toda la información relevante de nuestro proyecto.(se tratará a fondo más adelante)

README.md: Este es un archivo con extensión .md( Markdown), por defecto es el archivo llamado por NPM para mostrar un resumen y/o instrucciones de instalación de nuestro módulo o paquete Node.js.


No es la finalidad de este documento crear módulos en npm, solo saber como usarlos y ensamblarlos en nuestra aplicación, no obstante en la web oficial de esta tecnología se explica de forma detallada como hacerlo.


INICIANDO LA APLICACIÓN

Anteriormente hemos ejecutado pequeños bloques de código separados entre si, pero con las diferentes herramientas descritas ya tenemos la capacidad de plantear el scaffolding de nuestra aplicación. Existen soluciones de alto nivel como yeoman que nos abstraen casi por completo de la lógica interna de directorios de nuestra aplicación y que en posteriores aplicaciones el desarrollador puede implementar para agilizar aún más su implementación, no obstante en este acercamiento considero oportuno organizar la aplicación de una forma más “artesanal” para así conseguir una comprensión más profunda.

El primer paso es iniciar nuestro proyecto, creamos la carpeta que lo alojará y nos dirigimos a su ruta desde una terminal. después escribimos:

	npm init

Tras ejecutar este comando se nos pedirá que insertemos los metadatos de nuestra aplicación, nombre de los desarrolladores, versión en la que se encuentra, nombre de la aplicación, una breve descripción, repositorio git (en el mundo node git es uno de los pilares fundamentales), licencia, etc. Una vez finalizado se nos mostrará un resumen en formato json de los valores añadidos. Este json es guardado como un documento en nuestra aplicación. bajo el nombre de package,json.


Package.json: es el pilar de trabajo de npm, en el se encuentran los módulos instalados, sus versiones y toda la información resumen de nuestra aplicación.


con nuestro proyecto iniciado podemos proceder a añadir las librerías que deseemos  a nuestra aplicación.

Para instalar una nueva libreria solo hemos de ejecutar:
	
/*
		npm install <nombre de la libreria>
	*/
	npm install moment

Con esta ejecución hemos añadido a nuestro proyecto la librería moment.js que se encarga de facilitarnos el manejo de fecha | hora dentro de nuestra aplicación.

al haber añadido nuestra primera librería a la aplicación se nos ha generado el directorio node_modules. El cual almacenará todas las librerías requeridas de nuestra aplicación. Si usamos git conviene añadir este directorio a .gitignore pues en grandes aplicaciones puede pesar mucho.

Si además deseamos que la declaración de nuestra libreria se guarde en el fichero package.json para así poder migrar de forma sencilla nuestra aplicación usaremos 


	npm install --save <nombre del paquete>

Cuando guardamos la información de las librerías en package.json es una buena práctica separar las librerías de producción de nuestra aplicación con las librerías de desarrollo por lo tanto cuando usémos librerías que sólo serán utilizadas para ejecutar test, o tareas de desarrollo usaremos:

npm install --dev <nombre del paquete>
