#Estructura de Ángular.js

En este capitulo trataremos la sintaxis y lógica que sigue angular para generar las web dinámicas. 

###Módulos

Es el primer concepto a introducir. El módulo es la forma que tiene *Ángular.js* de enpaquetar el código relacionado entre sí baje el mismo nombre. El analogo en java podría ser una clase. El módulo está compuesto de dos partes:

* Controladores, servicios, factorias y directivas. Que son las funciones y el código que recorrerá todo el módulo.

* Los módulos dependecias de las que depende el módulo actual. Los cuales son definidos en la declaración del mismo. Y nos permitiran expandir la funcionalidad de nuestro código.

La forma de definir un módulo es:

```javascript
    angular.module.('module-name', []);
```
        * El primer argumento es el nombre del módulo
        * El segundo argumento es un array con los nombre de los módulos que dependen de él

```javascript
    //Un módulo llamado fooModule que depende de los modulos lib1 y lib2:
    angular.module('fooModule', ['lib1', 'lib2']);
```

Si únicamente quisiseramos llamar a un módulo que está en otro fichero simplemente simplemente lo llamaríamos por su nombre:

```javascript
    angular.module.('module-name');
```

La línea anterior informa a *Ángular.js* de que hay un módulo que se llama module-name en alguna parte del DOM y que puede ser utilizado en este fichero


Para vincular un módulo a nuestro fichero html usamos dentro de la etiqueta que englobará el código html dominio:

```javascript
    ng-app="module-name"
```
Por ejemplo:

```html
    
    <html ng-app="module-name">
    
    <!-- Resto del código -->
    
    </html>
```
Los módulos puedes estar declarados como scripts dentro del código html o en ficheros de scripts que son importados 

dentro del código, la segunda opción es la
Más elegante, sobre todo para aplicaciones de gran embergadura.


###Controlador

Ahora que tenemos el envoltorio llenemoslo con las diferentes funciones que deseamos. de ello se encargará cada uno de nuestros controladores. Sus tareas son:

* recolectar los datos del servidor para servirlos en la vista.

* decidir que partes de la lógica se muestran al usuario.

* Decidir con qué componentes dinámicas de la vista se muestran al usuario.

* Controlar la interacción del usuario con la vista; validar campos, formatos, etc.

para poder usar un controlador primero hay que haber declarado un modelo. Luego dentro de la etiqueta que limitará la jurisdicción de nuestro controlador realizaremos la llamada:

```javascript
     <html ng-app="module-name">
    
    <!-- Cabeceraa -->
    
    <body ng-controller=
     <!-- Código que podrá tratarse dentro del controlador -->
    <h1>{{title}}</h1> 
    </body> 
    </html>
```


Después añadiremos las funcionalidades del controlador dentro bajo la declaración del modelo de nuestra aplicación:

    app.controller("nombreCtrl", function(){
    	
    	$scope.title = 'pagina de prueba para el controlador'
    });

Ahora cuando se cargue la web, al llegar al body se cargará el controlador y se llamara a *$scope* que es el objeto que se encarga de comunicar el controlador con la parte de la vista. En el se cargarán todas las diferentes propiedades que deberemos mostrar más tarde.

###Directivas

Las directivas nos permiten hacer nuestra aplicación más modular aún. Su lógica está basada en declarar un bloque de la aplicación que esté vinculado a un código html y a un controlador especifico.

Su código estaría basado en :

```javascript
        app.directive('nombreDirectiva', ['$librerias a importar', function(){
    	    return {
    		    restrict: 'E',
    		    templateUrl: '/views/create-user.html',
    		    controller: function(){
                //Datos del controlador 
            }
        }]);
```
*  **restrict** se encarga de decir el tipo de dato, en este caso es un tag html y será el que se suela usar.

* **templateURL** es la dirección del código html que se renderizará al llamar a la directiva desde la vista html.

* **controller** Haces las funciones de controlador principal dentro del template definido.

Para instanciar la directiva dentro de la vista usariamos el siguiente tag:

    <nombre-directiva></nombre-directiva>
    
Notese que en la vista se convierte la nomenclatura camelCase por - antes de donde iría la letra mayuscula.

Una vez que se manejan las directivas son muy útiles para desarrollar códigos faciles de mantener.


###Factorias

Son usados para compartir objetos entre diferentes controladores y su nomenclatura es muy simple

```javascript
    app.factory("descargasFactory", function(){
        var descargasRealizadas = ["Manual de Javascript", "Manual de jQuery", "Manual de AngularJS"];

        var objetoParaCompartir = {
            fookey : 'fooValue',
            fookey1; 'fooValue1'
        }
        return objetoParaCompartir;
    });
```
