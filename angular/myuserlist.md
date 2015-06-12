##Cliente Angular.js en myuserlist

En este capitulo desarrollaremos el cliente de del pequeño servidor que creamos con anterioridad. Dicho cliente estará comprendido por dos componentes de Ángular.js; un pequeño formulario para crear nuevos usuario y una tabla que nos mostrará la lista de todos ellos. 

Lo primero que haremos será descargar los framework de bootstrap (para hacer las agradable a la vista la web) y Ángular.js y los introduciremos en la siguiente ruta:

    /site/public/lib
    


Bootstrap es simplemente un framework css con una serie aspectos visuales que nos ayudará a hacer nuestra web más estetica de forma muy simple.

Al descargar bootstrap hemos de añadir además de la librería javascript el directorio que contendrá la hoja de estilos.
 
 Esta hoja la será incluida en:
 
    /site/public/styles
 
 
Nuestro controlador de Ángular.js sera creado bajo el nombre de *controlPanelController.js* en el directorio:

    /site/public/controller
 
 
 -----------------------------------------------
    

Lo siguiente será crear la vista web que hará las funciones de panel de contol. el fichero .html será creado dentro del siguiente directorio con el nombre de *controlPanel.html*

    /site/public/views/
 
 Lo primero que haremos será crear nuestra cabecera e importar las librerias y nuestro cotrolador, así como vincular nuestro modulo con la web:
 
```html
    <html ng-app="app">
    <head>
       <link rel="stylesheet" href="/styles/bootstrap.min.css" type="text/css">        
      <script src="/lib/jquery-1.11.3.min.js"></script> 
      <script src="/lib/bootstrap.min.js"></script>
      <script src="/lib/angular.min.js"></script>
      <script src="/controllers/controlPanelController.js"></script> 
    </head>
```

 
 


