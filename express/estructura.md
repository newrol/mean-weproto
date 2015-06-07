##Estructura de la librería

Él código de express está estructurado de la siguiente forma:

* **/lib/application.js:** es la interfaz principal de express. Navengando en su interior se puede descubrir como el middleware es enlazado dentro o como las vistas son renderizadas.

* **/lib/express.js:** aquí dentro se le añade funcionalidad a *connect* con */lib/application.js* y se devuelve una función que puede ser usada por *http.createserver* a la ejecución actual de express.js

* **/lib/request.js:** 