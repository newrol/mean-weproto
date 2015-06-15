##Características

Muchas de las funcionalidades que nos aporta *Express.js* serían implementables sin grandes costos de tiempo y esfuerzo sin él. No obstante conforme la aplicación va creciendo se agradece tener de un gestor de herramientas en tiempo de ejecución tan potente.

*Express.js* busca ser nuestra herramienta de "Scaffolding" dentro de la aplicación. Es decir que nos basemos completamente el él para crear el esqueleto de nuestra aplicación.

dentro de *Express.js* trabajaremos de forma constante con dos objetos; Request y response. Ellos son los encargados de de recibir los datos de la petición web, y de servir la respuesta. Por lo tanto será de vital importancia tener un concepto general de ellos:

* **request:** Suele ser pasado como parámtro a un callback, y él almacena las propiedes de la petición web: las cabeceras, los parámtros de entrada etc. Está basado en el objeto *htt.IncomingMessage* de node.js  Sus propiedades son:

    * **req.params:** es un array que contiene los llamados parametros de ruta
    
    * ** req.param(name):** devuelve el el parametro de ruta o los parámetros GET o POST
    
    * ** req.query:** Es el objeto que provee los parametros de la consulta
    
    * ** req.body:** Contiene los parámetros POST
    
    * ** req.route:** Contiene información de la ruta actual
    
    * ** req.cookies:** Contiene las cookies pasadas por el cliente
    
    * ** req.headers** Contiene las cabeceras recibidas por el cliente
    
    * ** req.accepts** Es un método pade determinar qué es lo que el cliente acepta
    
    * ** req.ip:** La dirección ip del cliente
    
    * ** req.path:** La ruta de petición sin protocolo, host, port o query
    
    * ** req.host:** devuelve el hostname reportado por el cliente, esta utilidad no debería de ser utilizada pues corre riesgo de ser spoofeada y supone un riesgo a la seguridad
    
    * ** req.xhr:** una propiedad que devuelve *true* si la petición fue realizada desde una llamada AJAX
    
    * ** req.protocol:** muestra el protocolo usado para crear la petición(http, https...)
    
    * ** req.secure:** propiedad que develve *true* si la conexión es https
    
    * ** req.url:** esta propiedad devuelvela ruta y la query sin incluir el protocolo, host ni puerto.
    
    * ** req.acceptedlanguajes:** devuelve un array de todos los lenguajes que el cliente prefiere.
    
* **Response:** Suele ser pasado como parámtro a un callback, Este objeto alamcena las propiedades de la respuesta que se le enviará al cliente tras su petición. Está basadop en el objeto *http:ServerResponse* de node.js. Sus propiedades son:

    * **rest.status(code):** establece el código http de la respuesta.
    
    * **rest.set(name, value):**  añade una cabecera
    
    * **rest.cookie(name, value, [opciones]):** añade una cookie que será almacenada por el cliente.  (requiere de un middleware)
    
    * **rest.clearCookie(name, [opciones]):** elimina la cookie. (requiere de un middleware)

    * **rest.redirect([status], url):** redirige al buscador
    
    * **rest.send(body) o rest.send(status, body):** añade la respuesta al cliente, suele ser en formato JSON
    
    * **res.json(json) o rest.json(status, json):** envia un JSON al cliente
    
    * **res.jsonp(jsonp) o rest.jsonp(status, jsonp):** envia un JSONP al cliente
    
    * **res.format(object):** esta función permite enviar diferentes contenidos dependiendo de la petición aceptada
    
    * **res.sendFile(path, [options], [callback]):** se utliliza para leer el contenido de un fichero y enviarselo al cliente
    
    * **res.links(links):** añade los links a la cabecera de respuesta
    
    * **res.render(view, [locals], callback):** contiene el contexto por defecto para renderizar la vista.
    
Para renderizar contenidos se puede usar *Handlebars* el cual nos permite crear vistas web dinámicas. Más no es el objetivo de deste documento usar a *Express.js* para servir de una web dinámica. Nosotros usaremos *Express.js* para servir la api rest que nos permitirá obtener el contenido dinámico con una interfaz mutiplataforma y adaptada completamente al formato de *Json* que estamos utilizando durante toda la aplicación. En el entorno de desarrollo usaremos *express.js* y node.js para servir el contenido estático de la web pero el programador ha de saber que para entornos de produccion esta practica no es aconsejable pues *Express.js* no está optimizado para el contenido estático. Para entornos de producción lo ideal es usar un servidor *Ngix* por delante de express para gestionar las peticiones estáticas y hacer de proxy para redirigir las peticiones REST a express.