##Objetos y herencia.

En *Javascript* todos los objetos son mapas (diccionarios) en forma de clave (String) : valor. una línea clave:valor es considerada una propiedad.

ejemplo de objeto en javascript:

```javascript
    	var fooPerson = {
		name : ‘fooName’,
		age:	function(){
				return ‘fooAge’
			},
		interests: {
			football : false,
            basketball: true,	
		},
    };

```



Para añadir una propiedad al objeto mostrado anteriormente solo hemos de escribir:

```javascript
    fooPerson.height = 1,76;
```

Nuestra fooPerson tendrá el valor height dentro de su lista de propiedades.
Para acceder a cualquiera de estas solo hemos de llamarla de la siguiente forma:
*nombreObjeto.propiedad*, el valor de dicha propiedad nos será devuelto.


Para crear un constructor de objeto simplemente hemos de declarar una función con una serie de valores predeterminados, y llamarla como valor de una nueva variable haciendo uso new:

```javascript
    //Declaramos método constructor:
    function fooDao(){

        this.create = function(foo, callback){
            user.save(function(err, foo){
          	    if(err) callback(err);
          	    else    callback(foo);
            });
        };

        this.delete = function(foo, callback){
    	    user.remove(callback);
        };
    };

    //Creamos el objeto a partir de él. 
    var dao = new fooDao();

    //Llamamos a sus propiedades:
    dao.create( new foo, function(data){
	//programFlow usando data.
	};
	
	dao.delete(new foo, function(data){
		//programFlow usando data.
	};
```


La idea de la herencia de JavaScript se basa en prototipos, para ello se define un objeto (el objeto“padre” o prototipo) donde se aloja toda la información común que comparten todos los objetos de ese tipo (los objetos “hijos”). De esta manera se evita que cada objeto repita las propiedades y métodos comunes, lo cual ahorra memoria y agiliza la ejecución.

Más tarde para añadir propiedades heredadas a nuestro  solo hemos de añadir una nueva referencia vinculada al objeto construido.

Para añadir una nueva propiedad al prototipo de fooDao() solo tendríamos que escribir el siguiente código:

```javascript
    //Creamos el objeto que heredará las propiedades  a partir de él. 
    var inhertiDao = new fooDao();
	 
    //Le añadimos la nueva opción al protypo. 
    inheritDao.prototype.update = function(opportunity, callback){
         opportunity.update(callback);
    };

	//Para usarlo solo hemos de crear un nuevo objeto a partir del anterior:

	var extendedDao = new inheritDao();
	
    //Y llamar a la funcion:
    dao.delete(new foo, function(data){
		//programFlow usando data.
    };
```


Hasta aquí la introducción al lenguaje que usaremos a lo largo de toda nuestra aplicación web. En este capítulo hemos podido ver las diferentes peculiaridades de javascript y una introducción a cómo se estructura su código. En el siguiente introduciremos javascript en el lado del servidor y comenzaremos a “escribir” un ejemplo que nos guiará por toda nuestra aplicación.
