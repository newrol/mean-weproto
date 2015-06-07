##Caracteristicas

Muchas de las funcionalidades que nos aprta express.js serían implementables sin grandes costos de tiempo y esfuerzo sin él. No obstante conforme la aplicación va creciendo se agradece tener de un gestor de herramientas en tiempo de ejecución tan potente.

Express busca ser nuestra herramienta de Scaffolding dentro de la aplicación. Es decir que nos basemos completamente el él para crear e lesqueleto de nuestra aplicación.

dentro de express trabajaremos de forma constante con dos objetos; Request y response. Ellos son los encargados de de recibir los datos de la petición web, y de servir la respuesta. Por lo tanto será de vital importancia tener un concepto general de ellos

* **request:** Suelse ser pasado como parámtro a un callback, y él almacena las propiedes de la petición web: las cabeceras, los parámtros de entrada etc. Sus propiedades son:

    * **req.params:** es un array que contiene los llamados parametros de ruta
    
    * ** req.param(name):** devuelve el el parametro de ruta o los parámetros GET o POST
    
    * ** req.query:** Es el objeto que provee los 