##Estructura de la librería

Él código de *Express.js* está estructurado de la siguiente forma:

* **/lib/application.js:** es la interfaz principal de *Express.js*. Navengando en su interior se puede descubrir como el middleware es enlazado dentro o como las vistas son renderizadas.

* **/lib/express.js:** aquí dentro se le añade funcionalidad a *connect* con */lib/application.js* y se devuelve una función que puede ser usada por *http.createserver* a la ejecución actual de *Express.js*.

* **/lib/request.js:** se encarga de extender el objeto http.IncomingMessage para proveer un sistema robusto de peticiones.


* **/lib/response.js:** se encarga de extender el objeto http.ServerResponse para proveer un sistema robusto de respuestas.

* **/lib/route.js:** provee de un soporte básico para rutas("nosotros usamos nuestro fichero properties pues al usar este sistema y querer usar test unitarios tendríamos problemas de rutas").
