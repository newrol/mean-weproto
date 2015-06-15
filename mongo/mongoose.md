##Mongoose

###Descripción

*Mongoose* es la herramienta de modelado de objetos para *MongoDB* y *Node.js*, lo que esto significa en terminos prácticos que tu solo tendrás que definir un modelo de datos en un solo lugar; tu código. Y este será portado directamente a la base de datos de *mongoDB* a la que estés conectado en ese momento. 

Podríamos elegir el driver básico de *MongoDB* para *Node.js*, pero este elemento es solo recomendable en entornos críticos con unas características especiales.

*Mongose* es bueno para:

*  Cuando se buscar interactuar con un esquema de datos estructurados , ya que con nuestro esquema predefinido podremos realizar la mayoría de las tareas.

* Aumentar la abstracción de la tecnología que usamos y simplificar el uso de la persistencia en *Node.js*.

* Trabajar directamente sobre los ficheros JSON que nos devuelve *MongoDB* 

* Apollarnos en las queries que utilizamos, pues las consultas básicas que podamos hacer en la base datos vienen predefinidas en el esquema.

*Mongose* no es bueno en:

* datos que no obedecen a esquema.

* Documentos aleatórios.

* pares clave valor puros.

###Instalación

*Mongoose* puede ser instalado desde el gestor de paquetes *Npm* 
    
    npm install --save mongoose
    
###Implementación

Para comenzar a usar mongoose en nuestro código node.js primero hemos de importar el driver descargado a nuestro código:

```javascript
    var mongoose   = require('mongoose');
```

Después nos conectaremos a la base de datos que deseemos:

```javascript
    var fooDatabaseUri = 'mongodb://myBaseDeDatos';

    mongoose.connect(fooDatabaseURI);
```

    
Con *Mongoose* no hemos de precuparnos en un principio por la gestión de abrir y cerrar la conexión de la base de datos pues esta utiliza un pool de conexiones por defecto y el se encarga de gestionarlas.

El siguiente paso es crear el esquema de datos que utilizaremos:

```javascript
    var valueSchema = new mongoose.Schema({
        title  : { type: String, required: true, unique: true },
        value :  { type :String, required:true },
    });

```
Con nuestro esquema creado solo tendremos que crear un objeto envoltorio del mismo:

    var Value = mongoose.model('value', valueSchema); 
    
Para crear nuevas instancias en base a value usaremos el *new*

    var value1 = new Value;
    var value2 = new Value;
    
Ahora tenemos dos valores dieferentes con sus propiedades. Ahora podremos ponerle titulo y valor a nuestros objetos:

    value1.title = "titulo1";
    value2.title = "titulo2";
    
El siguiente paso es guardar nuestros valores en la base de datos. En el anterior capitulo mostramos como trabaja mongoDB como su shell base y usando las funciones allí mostradas podríamos hacer nuestras consultas si estubieramos usando el driver básico. Pero como mongoose se nos simplifica mucho esta tarea:

Primero guardaremos value1:

    value1.save(function(err){
      if(err) console.log('No se ha podido guardar este valor');
    });
 
Al ejecutar la función *save()* se nos devolverá un primer callback en caso de error y un segundo con objeto guardado y su correspondiente _id asignado, en este caso solo queremos saber cuando se ha producido un error.

Borremos value1:

    value1.remove(function(status){
        console.log(status);
    });
  
en caso de desear actualizar con nuevos valores solo tendríamos que modificiar el parametro del objeto existente y llamar a su función update.
  
    this.update = function(opportunity, callback){
        opportunity.update(callback);
    };
    
En cambio para realizar una consulta no usaremos un objeto creado, si no que utilizaremos el objeto envoltorio.

    //Primero construimos la query sobre el modelo.
    var query = Value.findOne({'title' : 'titulo1'});
      
    //después ejecutamos la query:
    
    query.exec(function(err, values){
        if (err) Console.log('ha sucedido un error');
        else console.log(values);
    });    
    
En ese caso se nos devolverá un objeto con los valores de value1, si la consulta devulveria más de uno lo que se nos devolvería sería una colección de todos los valores encontrados.

Como podemos ver mongoose facilita mucho la interación con la base de datos y abstrae nuestro esquema de datos de las diferencias entre las dos plataformas. Esta funcionalidad hace de mongoose + node.js un planteamiento perfecto a la hora de prototipar apliaciones que requieran una conexión a  una base de datos.
    