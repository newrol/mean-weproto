##Características

*Angular.js* se autodescribe como un framework MVC superheróico. Y esta es su pricipal característica. nos abstrae toda la lógica de la aplicación de la página principal simplemnte añadiendo nuevas etiquetas al lenguaje html que vincularán la vista con el modelo y controlador. Está escrito completamente en *Javascript* por lo que la integración con la web es completa.

Antes de continuar describiendo *Angular.js* expliquemos qué es el modelo vista controlador. En nuestra aplicación *myuserlist* lo hemos estado implementando en cierta manera sin mostrarlo explicitamente, pues hemos tratado de separar interfaz rest del modelo de *MongoDB* así como del controlador que une a la vista con la lógica. MVC se divide en :

* **Modelo:** Es la fuerza motriz de la aplicación, que generarlmente es el conjuto de datos que trabajan por detrás de la aplicacion. 

* **Vista:** es la inter faz de usuario, y el medio mediante el que él interacciona con la aplicación. Es un elemento dinámico y es genrado en base al controlador de la aplicación.

* **Controlador:** es quien maneja las acciones entre nuestra lógica de negocio y la capa de presentación. El controlador básicamente se encarga de definir que partes del modelo se mostrarán por pantalla y como se interactuará con estos datos.

*Angular.js* divide su filosofía en 5 puntos principales que aportan a los desarrolladores la capacidad de crear grandes y complejas aplicaciones de forma sencilla.

*   **Orientado a datos:** En el cliente compartiremos el mismo modelo de datos que poseemos en el sevidor y por lo tanto podremos operar tras las pertinentes peticiones al mismo.

* **Declarativo:** con un solo vistazo a nuestra web podremos interpretar el código que la ejecuta.

* **Separación de conceptos:** Al implementar el MVC

* **Inyección de dependencias:** Esto lo caracteriza de otros frameworks con el mismo propósito.  la inyección de dependecias  está presente en todos los apartados de *Angular.js* y la podremos implementar de forma independiente en cada módulo que implementemos.
* 
**Extensible:** las directivas que creemos podremos integrarlas con otros framework *como boostrap* o *jQuery.ui*.


Al estar basado en este esquema y por su estructura Angular.js aporta una serie de beneficios que numeraremos a continuación:

1. 
Nos permite crear aplicaciones de una sola página. gracias a los servicios podemos implementar AJAX a nuestro gusto conectándose a la correspondiente API.

1. 
Angular.js requiere solo unas pocas líneas de código para completar tareas si lo comparamos con *Javascript* puro o con *JQuery* (del cual puede beneficiarse).

1. 
Gran cantidad del código que se escribe en *Angular.js* estará enfocado en la lógica de negocio o en en el núcleo de la funcionalidad.

1. 
La naturaleza declarativa simplifica la tarea de escribir y mantener nuestra aplicación solo con mirar nuestro código html y los controladores.

1. 
los templates de *Angular.js* están escritos completamente en html de modo que los diseñadores lo tendrán facil para trabajar con el estilo de la aplicación.

Angular no tiene especiales requerimientos sobre el tipo de lenguaje usado en el servidor, simplemente ha de poder implementar Una api rest para aportar valores *Json*.

*Angular.js* es un complemento web y ha de ser usado como tal, es decir, no hemos de vernos obligados a implementar toda nuestra lógica con él. Podemos además utilizar otras tecnologías que lo complementen.



