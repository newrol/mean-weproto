##Primeros pasos con Express.js

El primer paso para usar *Express.js* es añadirlo al proyecto actual de node.js para ello usaremos npm:

    npm insstall --save express

Luego crearemos un sript sencillo con el siguiente código:

    var express = require('express');
    
    var app = express();
    
    app.set('port', process.env.PORT || 4000);
    
    // pagina de error 404 personalizada
    app.use(function(req, res){
     res.type('text/plain');
     res.status(404);
     res.send('404 - Not Found');
    });
    
    // pagina de error 500 personalizada
    app.use(function(err, req, res, next){
     console.error(err.stack);
     res.type('text/plain');
     res.status(500);
     res.send('500 - Server Error');
    });
    
    //Lanzamos el servidor
    app.listen(app.get('port'), function(){
     console.log( 'Express started on http://localhost:' +
     app.get('port') + '; press Ctrl-C to terminate.' );
    });

Con este código pondriamos a nuestra disposición una instancia de express.

Si quiseramos añadir rutas a la escucha solo tendríamos que usar la función *get()*:

```javascript
    app.get('/', function(req, res){
     res.type('text/plain');
     res.send('página principal');
    });
    
    app.get('/about', function(req, res){
     res.type('text/plain');
     res.send('Página de descripción');
    }); 
```

Estas dos rutas hay que añadirlas antes de las funciones de error 400 y error 500 pues nuestro servidor de express comenzará a buscar desde la primera hasta la última, si cuando recibe una petición su primer función a ejecutar es la 400 supondrá que no hay otras rutas en la aplicación y lanzará la respuesta de que no se ha encontrado la ruta seleccionada.

En este caso estamos añadiendo la ruta principal y la típica página de *about*. cabe decir que estamos enviando los textos planos descriptivos de cada aplicación. *'página principal'* y *página de despcripción*.

Si quisieramos vincular la ruta de cada petición a un fichero web con código html simplemente deberíamos de enlazarnos a su ruta:

```javascript
    //Se añade el directorio raiz del fichero
    app.use(express.static(__dirname));

    //se añaden los enlaces
    app.get('/', function(req, res){
	res.render('index.html');
    });
    
    //se añaden los enlaces
    app.get('/about', function(req, res){
	res.render('about.html');
    });
```

de esta forma solo tendríamos que moldear nuestros ficheros html a placer para mostrar cada una de las páginas.

Express está preparado para mostrar webs dinámicas, para ello utiliza los renders jade o handlebars. Yo personalmente me decanto por el segundo, pues tiene una lógica muy parecida a jekill en ruby on rails. Esta clase de render html son muy útiles a la hora de generar blogs simples o demás contenido dinámico que vaya a generar código html en tiempo de respuesta a petición. Nosotros en este caso usaremos *angular.js* para los contenidos dinámicos de nuestra web, por lo que solo tendremos que enlazar el contenido estático y servirnos de express para generar la *API REST* responderá a nuestras peticiones








