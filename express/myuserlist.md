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
    require(properties.path + 'api/index')(rest);
    
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
    
Con nuestro servidor Configurado crearemos el controlador que unirá las consultas dao con la api rest. Para ello creamos el siguiente directorio:

    /app/controllers
    
Y dentro de él *userController.js* con el siguiente código:

```javascript
    var properties = require('properties').properties;							//Import properties file
    	 	
    var UserModel  	   =  require(properties.path + 'app/models/user').User; 
    var UserDaoModel    = require(properties.path + 'app/dao/userDao').UserDao	
    
    /*
    	UserController prototype
    	Callbacks status code based on http status codes http://en.wikipedia.org/wiki/List_of_HTTP_status_codes.
    */
    function UserController(){
    
    	var userDao = new UserDaoModel();
    
    	/*	
    		Create new user, test userName exists
    	*/	
    	this.createUser = function(user, callback){
    		userDao.create(user, function(data){
    			//if the result is an instance of userMongoose Schema it was created:
    			if(data instanceof UserModel) callback({status : 201, data : data}); //If user has been created return correct value 201 and the user.
    			else if (data.code === 11000) callback({status : 409, data: 'this user already exist'});
    			else{
    				console.log('error', " UserController: Could not Create user:" + data);
    				callback({status: 500, data: data});
    			} 	
    		});
    	};
    	
    	
    	/*
    		Find all users
    	*/	
    	this.findAllUsers = function(callback){
        	userDao.findAll(function(data){
        		if(data === null)callback({status: 204, data: 'There are not users'});
        		else if(data[1] instanceof UserModel) callback({status : 200, data : data});
        		else{
    				console.log('error', " UserController: Could not find All users:" + data);
    				callback({status: 500, data: data});
    			} 	 
        	});
      	};
    }	
exports.UserController = UserController;
```

Dentro de el controlador filtraremos los datos enviaos por el dao y los prepararemos para enviarlos con la correcta nomenclatura web dentro de la api.

La api será alojada en el directorio:

    /api

Dentro de api crearemos el fichero *index.js* el cual enlazamos en el script de servidor con express. Dentro de index se alojará el codigo que enlazará las diferentes rutas de la aplicacion con sus rutas. En este caso solo el enlace con la ruta *userApi*

```javascript
    var properties = require('properties').properties;   //Properties file
    
    
    /*
    	Module to define all calls to different rest routes 
    	defined in this folder in their own files.
    */	
    
    module.exports = function(rest){
    
    	require(properties.path + 'api/userApi')(rest);
    }
```

Para terminal añadiremos *userApi.js* dentro de */api*
Con las correspondientes rutas web y sus respectivas llamadas al controlador.

```javascript
    var properties = require('properties').properties;
    var  rest = require(properties.path + 'api/index').rest;
    
    var UserModel           = require(properties.path + 'app/models/user').User;
    var UserControllerModel = require(properties.path + 'app/controllers/userController').UserController;
    
    var userController = new UserControllerModel();
    
    	
    module.exports = function(rest){
    
    	rest.post('/user', function(req, content, callback){
    		var user = new UserModel();
    		user.setNick(req.body.nick);
    		user.setName(req.body.name);
    		user.setSurname(req.body.surname);
    		user.setMail(req.body.mail);	
    
    		userController.createUser(user, function(user){
    			callback(null, { id: user.data.id }, { statusCode: user.status });
    		});	
    	});
    
    
        rest.get('/allUsers', function(req, content, callback){
    		userController.findAllUsers(function(users){
    			callback(null, users.data.map(function(user){ return user}), { statusCode: users.status } );
    		});	
    	});
    };
```

Nuestro proyecto quedaría con el siguiente esquema de directorios:

```javascript
myuserlist
 \
  |-api
     \
      |-index.js
      |-userApi.js
  |-app
      \
       |-dao/
          \ 
           |-userDao.js
       |-db/
          \
           |-dbSchema.js
       |-models/
          \
           |-user.js
  |-site
      \
       |-myuserlist.js    
  |- package.json
  |-properties.js	
  |Gruntfile.js
  |node_modules 
  |*Diferentes ficheros git en caso de usarlo.
```

Al finalizar esta implementación ya dispondríamos un servidor node.js plenamente funcional. En el siguiente capitulo se tratará la implementación de un cliente rest.


