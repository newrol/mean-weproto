#Persistencia en MyUserList

En este capitulo procederemos a añadir la capa de persistencia de datos a nuestra aplicación laboratorio.

Lo primero que hay que hacer es instalar (en la web está la info), y comprobar que el servicio de *MongoDB* está en ejecución.

Después hay que instalar el driver de *Mongoose*:


    npm install --save mongoose
    
Podremos comprobar que en nuestro fichero *package.json* se ha añadido las siugientes líneas:

```javascript
    "dependencies": {
        "mongoose": "^4.0.5"
    }
```

Y que ne *node.modules* se ha añadido el directorio *Mongoose* con todos los valores. Ahora procederemos a crear nuestro esquema de datos.

Para ello en en directorio raíz añadiremos la siguiente ruta

    /app/db
    
Y dentro del directorio db un fichero llamado *dbSchema.js*. Dentro de db schema crearemos nuestro esquema de datos de *Mongoose*.

```javascript
    var mongoose   = require('mongoose');//Importamos Mongoose {http://mongoosejs.com}

    var userSchema = new mongoose.Schema({
        nick  : { type: String, required: true, unique: true },
       	name : { type :String, required:true },
    	surname   : { type :String, required:true },
    	mail : String,
    });
    //Con exports exportamos este objeto para hacerlo visible
    exports.userSchema = userSchema;
```

De esta forma habremos creado nuestro modelo de *Mongoose*. Pero para esta aplicación me gustaría añadir un modelo basado en este que aún nos abstraiga más de la nomenclatura de *Mongoose* y sea más intuitivo a la hora de ser usado.

Crearemos el directorio:

    /app/models

Y dentro de models el fichero *user.js*. Dentro de user crearemos el modelo que usaremos en nuestra lógica:

```javascript
    var properties = require('properties').properties;	//Import properties

    var mongoose   = require('mongoose');	
    var dbSchema   = require(properties.path + 'app/db/dbSchema')

    var User = mongoose.model('user', dbSchema.userSchema); 

	User.prototype.setNick = function(userNick){
		this.title = opportunityTittle;
	};
	
	User.prototype.setName = function(userName){
		this.header = opportunityHeader;
	};

	User.prototype.setSurname = function(userSurname){
		this.body = opportunityHeader;
	};


	User.prototype.setMail = function(userMail){
		this.photoPath = opportunityPhotoPath;
	};


	//El id lo podremos obtener pero dejaros que mongoose trate con el
	User.prototype.getId = function(){
		return this._id;
	}

	User.prototype.getNick = function(){
		return this.nick;
	}

	User.prototype.getName = function(){
		return this.title;
	};

	User.prototype.getSurname = function(){
		return this.surname;
	};

	User.prototype.getMail= function(){
		return this.mail;
	};
    //Exportarmos este modelo de usuario:	
    exports.User = User;
```


Al ir añadiendo métodos al prototype podremos llamarlos cuando creemos nuestro objeto a través de sus getters y sus setters (ver capitulo de herencia en javascript).


Con nuestro modelo creado nos quedaría crear nuestro script "CRUD" que alojará nuestras consultas.

El script se creará en la siguiente ruta:

    /app/dao

Bajo el nombre de *userDao.js*, y contendrá el siguiente código:

```javascript
    var properties = require('properties').properties;      // Import properties file
   // Import Oportunity model.
    var UserModel = require(properties.path + 'app/src/models/user').User;      

    /*
      Function userDao constructor.
    */
    function UserDao(){

          
          this.create = function(user, callback){
            user.save(function(err, user){
              if(err) callback(err);
              else    callback(user);
            });
          }; 
        
          this.delete = function(user, callback){
              user.remove(callback);
          };
        
          
          this.update = function(user, callback){
              user.update(callback);
          };
        
        
          this.findByNick = function(userNick, callback){
              var query = UserModel.findOne({'title' : userNick});
              
              query.exec(function(err, user){
                if (err) callback(error);
                else callback(user);
              });    
          };
        
          
          this.findById = function(userId, callback){
             var user = new UserModel();
        
              var query = UserModel.findOne({'_id' : userId});
              
              query.exec(function(err, user){
                if (err) callback(err);
                else callback(user);
              });    
          }
        
          this.findAll = function(callback){
            
            var query = UserModel.find({});
        
            query.exec(function(err, users){
              if(err) callback(err);
              else callback(users);
            });
          };
    }
    exports.UserDao = UserDao
```

De esta forma lo que hemos hecho ha sido encapsular todas las consultas que realizaremos dentro de nuestra app en un solo fichero.

La estructura del proyecto hasta el momento sería:

```javascript
myuserlist
 \
  |-app/
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
  |- package.json
  |-properties.js	
  |Gruntfile.js
  |node_modules 
  |*Diferentes ficheros git en caso de usarlo.
```



    