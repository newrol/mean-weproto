##API REST con express

###¿Qué es una API REST?

Es un estilo de arquitectura software para sistemas hipermedia distribuidos como la World Wide Web. El término se originó en el año 2000, en una tesis doctoral sobre la web escrita por Roy Fielding, uno de los principales autores de la especificación del protocolo HTTP y ha pasado a ser ampliamente utilizado por la comunidad de desarrollo.

en la actualidad se usa en el sentido más amplio para describir cualquier interfaz web simple que utiliza XML y HTTP, sin las abstracciones adicionales de los protocolos basados en patrones de intercambio de mensajes como el protocolo de servicios web SOAP.

Una api rest es prácticamente imprescidible a la haora de utilizar tecnologías como *Ángular.js* o para usar servidores que suministrarán de una determinada lógica a clientes heterógeneos; aplicaciones nativas móviles al mismo tiempo que web, wearables, etc.

###Caracteristicas de una API REST

* **Un protocolo cliente/servidor sin estado:** cada mensaje HTTP contiene toda la información necesaria para comprender la petición. Como resultado, ni el cliente ni el servidor necesitan recordar ningún estado de las comunicaciones entre mensajes. 

* **Un conjunto de operaciones bien definidas que se aplican a todos los recursos de información:** HTTP en sí define un conjunto pequeño de operaciones, las más importantes son POST, GET, PUT y DELETE.

* **Una sintaxis universal para identificar los recursos:** En un sistema REST, cada recurso es direccionable únicamente a través de su URI.


* **El uso de hipermedios, tanto para la información de la aplicación como para las transiciones de estado de la aplicación:** la representación de este estado en un sistema REST son típicamente HTML o XML. Como resultado de esto, es posible navegar de un recurso REST a muchos otros, simplemente siguiendo enlaces sin requerir el uso de registros u otra infraestructura adicional.



###Debug de una API REST

Existen gran antidad de plugins para navegadores que nos aportanuna interfaz simple para testear nuestra apli rest.

Un ejemplo sería *Advanced REST client* para google chrome. Usándolo solo hemos de insertar la ruta web de nuestra api, seleccionar el tipo de petición y el nos devolverá la respuesta por pantalla.

###Implementación en express

En una api rest se suele enviar el resultado de una operación lógica quien solicitó la información. 

En el siguiente código mostraremos como añadir una ruta api a nuestro servidor de express.

Lo primero será añadir las librerias necesarias al código:

```javascript
    //Con connect rest añadimos la funcionalidad rest a nuestra aplicación.
    npm install --save connect-rest
    
    //Con body parser wrapeamos el body de las peticiones a json
    npm install --save body-parser

```

    
Después añadimos rest a express:

```javascript
    //Importamos la librería
    var rest = require('connect-rest');
    
    //Definimos la configuración de la api
    
    var apiOptions = {
        context: '/api'
    }
    
    //añadimos rest al middleware:
    app.use(rest.rester(apiOptions));
    
    
    //añadimos una ruta get:
    rest.get('/fooGet', function(req, content, cb){
        foo.find({ queryValue: true }, function(err, fooFound){
            if(err) return cb({ error: 'Internal error.' });
            cb(null, fooFound.map(function(a){
                return {
                    key1: a.key1,
                    key2: a.ke2,
                };
            }));
        });
    
    //añadimos una ruta post:
    rest.post('/attraction', function(req, content, cb){
        var a = new foo({
            name: req.body.key1,
            description: req.body.key2,
        });
         a.save(function(err, a){
             if(err) return cb({ error: 'Unable to add foo.' });
            cb(null, { id: a._id });
        });
    });
```

En este código hemos añadido una consulta y un create por medio de dos rutas rest. De modo que para realizar las tareas relacionadas con estas dos rutas hemos de configurar los clientes de la forma correcta para que se conecten a la interfaz REST. Se recomienda encarecidamente documentar correctamente esta parte de la aplicación pues será la interfaz sobre la que los clientes operaran para obtener datos.

    
