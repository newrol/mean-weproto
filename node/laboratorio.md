##El laboratorio: myuserlist.


Ya se ha profundizado lo  suficiente en el lenguaje javascript y su entorno de ejecución en servidor para comenzar a crear un proyecto que nos conduzca a ir poner en práctica todas las tecnologías aquí se describen.

El código completo del proyecto se encuentra en github, en la siguiente URl:
https://github.com/newrol/myuserlist

La funcionalidad que incluirá esta aplicación será muy sencilla. En ella mostraremos desde una web un listado de diferentes usuarios que se encuentran almacenados en una base de datos. y cubrirá las siguientes áreas:

* **Persistencia.**

* **consultas a BBDD.**

* **API rest para servir los datos en web.**

* **Controlador consultas-API.**

* **Servidor web para las rutas Rest y web básica donde se imprimirá la información.**

* **Cliente web html básico.**

* **llamadas a la API rest desde el cliente para mostrar los datos.**

* **Test unitarios a dao, controlador y Rest.**

* **Control autenticación y sesiones para realizar las consultas.**


Al final de cada explicación de una nueva funcionalidad se le añadirá el código correspondiente al nuestra aplicación.

En este capítulo podremos iniciar la aplicación y enlazarla a grub, además de crear nuestro archivo properties para una mejor organización:


Primero nos dirigiremos con una terminal a la ruta de myuserlist y iniciaremos npm y rellenaremos el formulario con los parámetros correspondientes.

	npm init
    
    npm install --save grunt
    
Después crearemos el fichero properties.js con el pah de nuestra aplicación.

	/*	
        Properties.js
	*/
	module.exports.properties = {
		//absolute project path route:
		path : __dirname + ‘/’,
	};

Para terminar añadiremos el Gruntfile.js para gestinar la configuración de grunt.

```javascript
        /*	
        Gruntfile.js
	*/
	var fs = require('fs');

module.exports  = function(grunt) {

   //Grunt task to set build the basic project configuration:
	grunt.registerTask('build', 'My "default" task description.', function() {
		//Create a symbolic link to set properties.js file as a general library:
  		fs.symlinkSync(__dirname + '/properties.js', __dirname + '/node_modules/properties.js');
	});
};
```
Después hemos de iniciar nuestra "librería" propiedades con:

    grunt build




Hasta el momento nuestra jerarquía de directorios en el proyecto quedaría se mostraría de la siguiente forma:



```javascript
myuserlist
 \
  |- package.json
  |-Gruntfile.js
  |-properties.js	
  |*node_modules -> invisible pues no se ha añadido librerias
  |*Diferentes ficheros git en caso de usarlo.
```