##GRUNT

Durante el desarrollo de nuestro servidor y en su entorno de ejecución tendremos que realizar ciertas tareas que no están directamente relacionadas con la ejecución principal de nuestro productor pero si tendremos que hacer tareas de mantenimiento, lanzamiento test, mantenimiento de las claves de cifrado etc. Para todas estas tareas tenemos a *Grunt*, todo un ecosistema con plugins prediseñados que nos simplicarán ciertas tareas. 

Para aquellos que solo se han relacionado con lenguajes como *Java* o *C#* no tienen experiencia en este tipo de software, pero en el siguiente ejemplo podremos ver la gran utilidad que tiene, y a lo largo de este documento usaremos *Grunt* para ayudarnos en ciertas tareas de desarrollo, despliegue y mantenimiento de nuestro ejemplo.

Una de las deficiencias que trae *Node.js* por defecto es su gestión de las rutas relativas a la hora de importar scripts desde distintos documentos. Una aplicación web con una funcionalidad media requerirá de varios módulos divididos en diferentes ficheros y a su vez organizados en diferentes directorios. 

A continuación mostraré el problema que se plantea y como el gestor de tareas *Grunt* puede ayudarnos a solventarlo.

para importar dichos ficheros solo hemos de usar la palabra reservada de node require y llamar a los ficheros con funciones o constructores que deseemos invocar en el fichero actual utilizando la nomenclatura de *Unix* de ../ para acceder a los ficheros superiores.

Veamos cómo sería una llamada directa desde el fichero A hasta el fichero B:

jerarquía:
```javascript
Raíz
 \
  |- lib/
      \
       |- fileB.js
  |- app/
      \
       |- folder1/
		\
		 |- fileA.js
 
```
Para importar el fichero:

```javascript
    var fileB = require(‘ ../../lib/fileB’);
```

Como se puede apreciar no parece una forma muy intuitiva de importar ficheros y en grandes aplicaciones este código puede ser tedioso de mantener.

Otra opción podría ser usar toda la ruta absoluta:

```javascript
    var file = require(‘ruta/desde/home/pasando/por/raíz/lib/fileB’);

```

A simple vista, aunque muy larga puede parecer una forma válida de importar ficheros y saber de un vistazo donde se encuentran, pero el problema comienza cuando otro desarrollador trabaja en este proyecto desde su máquina con su propia jerarquía de directorios. Cada vez que se hiciera pull desde git o se transfiriera el código de una máquina a otra habría que cambiar todas las rutas de todos los ficheros.

Necesitamos una forma de importar los ficheros partiendo de la ruta relativa del proyecto. 

Anteriormente hemos importado las librerías base de node.js por su nombre, así como las que se añaden desde *Npm*. Y es que todo aquello que reside en el directorio node_modules,  es decir todos los módulos pueden ser llamados directamente por su nombre. Una opción podría ser crear un enlace simbólico a cada fichero de nuestra aplicación dentro de  node_modules. Esta práctica añadiría mucho ruido dentro de nuestra aplicación y mantendríamos el problema de los movimientos realizados por *Git*, y es que el directorio node_modules  suele estar incluido en *.gitignore*, por lo tanto todos los cambios realizados dentro del directorio de librerías no se “commitearían”.

La solución es generar un fichero de propiedades de nuestra aplicación que incluya la ruta absoluta hasta dicha raiź y un vínculo de ese único documento a node_modules. Después apoyándonos con grunt crear el enlace simbólico a ese documento cuando iniciemos el proyecto por primera vez y así disponer de dicha ruta en todos diferentes entornos que se ejecutará la aplicación.


Procedamos a crear nuestro documento properties.js con la información requerida:

```javascript
    /*	
    Properties.js
	*/
	module.exports.properties = {
		//absolute project path route:
		path : __dirname + ‘/’,
	};
```

Con module.exports hacemos visible nuestro objeto properties desde el exterior.
__dirname es una propiedad de node.js que nos devuelve un valor String con la ruta absoluta hasta el directorio en el que nos encontramos.

Este fichero properties no será muy útil en el futuro para ir añadiendo más propiedades de configuración a nuestra aplicación como pueden ser las url de la base de datos, ficheros de log, etc. Iremos haciendolo crecer durante el desarrollo de la aplicación de ejemplo.

Ahora para llamar a fileB desde fileA haríamos algo así.


```javascript
	//importamos nuestro propierties para acceder a la ruta:
	var properties = require(properties).properties;
	
	//importamos el fichero B valiendonos de properties:
	var fileB = require(properties.path + ‘lib/fileB’)
```

Ejecutar el código ahora nos daŕia un error de properties no encontrado pues aún no hemos creado el enlace a Node_modules. Procedamos.

Primero instalaremos *Grunt* en nuestro equipo. A diferencia de *Npm*, con *Grunt* necesitaremos realizar dos pasos, instalar el entorno de ejecución global para poder hacer uso de *Grunt* en nuestro equipo y además iniciarlo para cada proyecto donde queramos creárlo.

Para instalar *Node.js* en nuestra computadora, llamaremos a la siguiente orden desde terminal:

    npm install -g grunt	
    npm install -g grunt-cli	

Con -g ordenamos a *Npm* que instale *grunt-cli* en el sistema.

con *Grunt* instalado hemos de añadir el fichero *Gruntfile.js*, dentro de la raíz de nuestro proyecto, que se encargará de almacenar toda la configuración de los plugins de *Grunt* que añadamos y las diferentes tareas.
	
```javascript
    /*	
        Gruntfile.js
	*/
	module.exports  = function(grunt) {
		
		//Task to create a simbolic link from properties.js tonode_modules:	
		grunt.registerTask('propertiesLink', '*Build Task*. Create a symbolic link to 
            set properties.js file as a general library.', function() {
  				fs.symlinkSync(__dirname + '/properties.js', __dirname +  
                    '/node_modules/properties.js');
		});

		
		//Grunt task to set build the basic project configuration:
		grunt.registerTask('build', 'Execute the build tasks', ['propertiesLink', 
            'genKey']);

	};
```
	
Con esta configuración tendríamos a nuestra disposición la tarea build para crear el enlace simbólico en properties. de forma que solo tendríamos que ejecutar esta orden cuando nos clonamos del repositorio o cuando movemos el proyecto de un pc a otro.

para ejecutar la orden hemos de dirigirnos con nuestra terminal al directorio ráiz del proyecto y lanzar el siguiente comando:

    grunt build 
  
Y tendríamos properties enlazado a node_modules y nuestro problema con los “imports” solventado.

En los siguientes capítulos, conforme se vayan mostrando nuevas funcionalidades se extenderá en el uso de *Grunt*.
