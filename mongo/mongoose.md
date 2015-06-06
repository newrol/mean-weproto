##Mongoose

Mongoose es la herramienta de modelado de objetos para mongoDB y node.js, lo que esto significa en terminos prácticos que tu solo tendrás que definir un modelo de datos en un solo lugar; tu código. Y este será portado directamente a la base de datos de mongoDB a la que estés conectado en ese momento. 

Podríamos elegir el driver básico de mongoDB para node.js, pero este elemento es solo recomendable en entornos críticos con unas carácteristicas especiales.

Mongose es bueno para:

*  Cuando se buscar interactuar con un esquema de datos estructurados , ya que con nuestro esquema predefinido podremos realizar la mayoría de las tareas.

* Aumentar la abstracción de la tecnología que usamos y simplificar el uso de la persistencia en node.js.

* Trabajar directamente sobre los ficheros JSON que nos devuelve mongoDB 

* Apollarnos en las queries que utilizamos, pues las consultas básicas que podamos hacer en la base datos vienen predefinidas en el esquema.

Mongose no es bueno en:

* datos que no obedecen a esquema.

* Documentos aleatórios.

* pares clave valor puros.

###Instalación

mongoose puede ser instalado desde el gestor de paquetes NPM 
    
    npm install --save mongoose
    
###Implementación

Para comenzar a usar mongoose en nuestro código node.js primero hemos de importar el driver descargado a nuestro código:
    
    var mongoose   = require('mongoose');
    
Después nos conectaremos a la base de datos que deseemos:

    var fooDatabaseUri = 'mongodb://myBaseDeDatos';
    
    mongoose.connect(fooDatabaseURI);
    
Con mongoose no hemos de precuparnos en un principio por la gestión de abrir y cerrar la conexión de la base de datos pues esta utiliza un pool de conexiones por defecto y el se encarga de gestioarlas.

El siguiente paso es crear el esquema de datos que utilizaremos:

    var valueSchema = new mongoose.Schema({
        title  : { type: String, required: true, unique: true },
       	value : { type :String, required:true },
    });
    

    