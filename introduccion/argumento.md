##Argumento del proyecto
	

“La mejor manera de empezar algo es dejar de hablar de ello y empezar a hacerlo” Walt Disney


En las siguientes líneas expongo como la metodología de desarrollo propuesta 
se ajusta a los requerimientos mostrados en el capitulo anterior.

-MongoDB: Será el encargado de la persistencia en disco de nuestro modelo 
de aplicación. Es un sistema de bases de datos nosql que está cogiendo mucha fuerza estos años y que junto a mongoose; el ODM( que usaremos reduciremos al máximo la brecha entre aplicación/base de datos. 

-Javascript: El lenguaje de programación. Es el pilar de este proyecto y su sintaxis 
será usada desde la configuración de mongoDB en nuestro servidor hasta el navegador web del usuario donde usaremos angular.js. Al usar un solo lenguaje para toda la aplicación web,  simplificamos notablemente el planteamiento y conocimientos base requeridos.

-Node.js:   Es el entorno de programación en la capa del servidor, gracias a su gestor 
        de paquetes y plugins, así como su administrador de tarea dispondremos     
        de un entorno de ejecución back end muy sólido y simple.

Express.js: es el framework web para node.js, gracias a él serviremos nuestra 
                    aplicación a nivel de red. Además nos ayudará con las rutas de nuestra Api   
       que nos permitirán una aplicación web mono página. Por lo tanto para       
       nuestro desarrollo no necesitaremos configurar tomcats ni apaches ni 
       demás software ejecutándose en contextos ajenos a nuestra aplicación.

Angular.js:    Es el framework que nos permitirá aplicar el mvc en 
javascript del lado del cliente, y ayudarnos en la gestión de datos entre la vista y el servidor de forma stateless. gracias a él abstraeremos la lógica de la vista.

Librerías suplementorias: Javascript posee gran cantidad de librerías que nos 
facilitarán el realizar las diversas tareas de autenticación (passport.js), test unitarios(mocha y chai), full rest (restler.js) y un largo etc que será tratado más adelante.


  
Todas estas tecnologías tienen varias características en común:

-software libre:   por lo tanto podremos ver su funcionamiento interno y pordremos ser capaces de implementarlas sin miedo a tener futuros conflictos de licencias. Más adelante posiblemente necesitemos versiones comerciales de estas librerías u otras tecnologías más consagradas. Pero ese es un paso que dista de los propósitos de este documento. Ahora buscamos tener un “algo” funcional que entregarle al mundo.

-Comunidad de usuarios activa. Por lo tanto cuando en nuestro proceso de implementación surjan dudas, que surgirán, podremos contar con el soporte de los usuarios y desarrolladores de estas tecnologías para conseguir una correcta implementación. Aquí stack overflow y github( donde residen los desarrollos de todas las tecnologías mencionadas anteriormente) son nuestros principales focos de información técnica específica.

-Son tecnologías muy jóvenes: la gran mayoría de ellas aún no ha llegado a la versión 1.0.0 en el momento de la redacción de este texto.  Por lo tanto requerirán un seguimiento de su desarrollo, pues, aunque sus cambios no suelen ser radicales podemos encontrarnos con ejemplos como angular,js que en su siguiente versión 2.0 cambiará completamente su sintaxis. Esta característica tiene el punto negativo de la atención extra requerida pero a su vez harán de nuestro proyecto competente con los requerimientos actuales.

 
-Son una apuesta directa de futuro:  el mundo del desarrollo las está planteando como una alternativa directa en contra de de otros esquemas  como ROR( ruby on rails) o LAMP.  Más adelante se mostrarán las cifras que sustentan este enunciado.



Estas son las bases del modelo de desarrollo planteado, ahora sin más preámbulos procederé a abrir nuestra nueva caja de herramientas y explicar en qué consiste cada una de ellas.