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
    
    <html ng-app="module-name"
    <
    
```



