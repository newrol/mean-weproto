##Estructura de la librería

Él código de express está estructurado de la siguiente forma:

* **/lib/application.js:** es la interfaz principal de express. Navengando en su interior se puede descubrir como el middleware es enlazado dentro o como las vistas son renderizadas.

* **/lib/express.js:** aquí dentro se le añade funcionalidad a *connect* con */lib/application.js* y se devuelve una función que puede ser usada por *http.createserver* a la ejecución actual de express.js

* **/lib/request.js:** se encarga de extender el objeto http.IncomingMessage para proveer unsistema robusto de peticiones.


* **/lib/response.js:** se encarga de extender el objeto http.ServerResponse para proveer unsistema robusto de respuestas.

* **/lib/route.js:** provee de un soporte básico para rutas("nosotros usamos nuestro fichero properties pues al usar este sistema y querer usar test unitarios tendríamos problemas de rutas").
*