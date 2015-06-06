##Node.js en acción


Para ejecutar código en node solo hemos de situarnos en la terminal del equipo con node previamente instalado  (ver web oficial) y teclear.
	
	node

se nos abriá un entorno de ejecución donde podremos “trastear” rápidamente o como si se tratara de la consola del navegador.

El ejemplo más utilizado para mostrar el poder de node.js es el del servidor web:

```javascript
    var http = require('http');
 
    http.createServer(function (request, response) {
        response.writeHead(200, {'Content-Type': 'text/plain'});
        response.end('Hello World\n');
    }).listen(8000);
 
    console.log('Server running at http://127.0.0.1:8000/');
```


Ejecutando este código desde nuestra terminal usando: 
	
	node nombreScript.js

habremos lanzado un servidor web al que podremos llamar por ejemplo usando telnet:
	
		telnet localhost 8000
 
El cual nos devolverá el String:

		hello world
Analicemos el código que hemos escrito:

		var http = require('http');  

Con la palabra reservada require importamos el módulo htt para
poder usarlo en adelante simplemente utilizando su referencia http.
	
	http.createServer(function (request, response) {
    		response.writeHead(200, {'Content-Type': 'text/plain'});
    		response.end('Hello World\n');
	})

Con http.createServer(...) llamamos a la función createServer del módulo http. dentro de la llamada “()” hemos declarado funcion(request, response) pues la función createServer devuelve dos callbaccks al ser ejecutada, y por lo tanto haciendo uso de la funcionalidad de javascript aprovechamos esas dos llamadas en el momento de declaración.
 
	response.writeHead(200, {'Content-Type': 'text/plain'});
    	response.end('Hello World\n');

En el cuerpo de la función llamamos a los dos parámetros de la función que tienen las propiedades writehead y end cada uno.

	.listen(8000);
	
Llama al objeto anónimo que hemos creado  que se crea para poner el servidor a la escucha del puerto 8000.

    console.log('Server running at http://127.0.0.1:8000/');


Se encarga de mostrar por pantalla el mensaje de desplieuge de servidor.

En este ejemplo hemos usado una librería específica de node.js a nuestro script le podremos añadir todas gramática de javascript pero con solo los módulos mostrados arriba y javascript no será suficiente para poder escribir y mantener nuestra aplicación, el gestor npm nos ayudará a ello.