##Express - API REST en MyUserList

En este apartado añadiremos *express.js* a nuestra aplicación laboratorio, así como de una api rest básica que nos permita consultar y añadir nuevos usuarios.

Lo primero es añadir las librerias necesarias para implementar express y la API.

    npm install --save express
    
    npm install --save connect-rest

    npm install --save body-parser
    
Después añadiremos la ruta principal que desplegará nuestro servidor:

    /site
    
y dentro el fichero *myuserlist.js* con el contenido de nuestro servidor.

```javascript
    var properties = require('properties').properties;	  
        express    = require('express'); 	  				
        rest       = require('connect-rest') 
        mongoose   = require('mongoose');
    	bodyParser = require('body-parser');
    
    //creación de la app con express:	
    var app        = express();
    
    //Definimos el puerto de actuación de express
    app.set('port', process.env.PORT || 3000);
    
    //añadimos la ruta estática:
    app.use(express.static(properties.path)); 	
    
    // conectamos nuestra instancia de mongoose
    mongoose.connect(properties.databaseURI);
    
    //valores generales de la api
    var apiOptions = {
    	context: '/api',
    }
    
    //añadimos body-parser para wrapear los formatos
    app.use( bodyParser.urlencoded( { extended: true } ) )
    app.use( bodyParser.json() );
    
    //añadimos las opciones de middleware:
    app.use(rest.rester(apiOptions));
    
    //Añadimos las rutas ala aplicación
    //en este caso las hemos trasladado a otro fichero
    //pues resulta una buena práctica en grandes   
    //aplicaciones
    require(properties.path + 'api/src/index')(rest);
    
    // error 400 personalizada
    app.use(function(req, res){
    	res.type('text/plain');
    	res.status(404);
    	res.send('404 - Not Found');
    });
    
    // error 500 personalizada:
    app.use(function(err, req, res, next){
    	console.error(err.stack);
    	res.type('text/plain');
    	res.status(500);
    	res.send('500 - Server Error');
    });
    
    
    //erro
    app.listen(app.get('port'), function(){
    	console.log( 'Express started on http://localhost:' +
    	app.get('port') + '; press Ctrl-C to terminate.' );
    });
```
El siguiente paso será añadir al objeto *properties.js*
la ruta de la base de datos para que mongoose pueda localizarla:

    databaseURI : 'mongodb://localhost/mobility',
    
