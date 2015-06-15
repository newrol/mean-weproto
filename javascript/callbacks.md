##Callbacks

	
Además de todas estas peculiaridades javascript tiene una cualidad que lo diferencia de los lenguajes convencionales; su naturaleza asíncrona. En javascript podremos diferenciar entre código bloqueante y código no bloqueante.

El flujo en un código bloqueante sería:

1. 
**toma los datos.**

1. 
**escribe los datos en la base de datos.**

1. 
**devuelve el mensaje de estado.**

1. 
**espera para la siguiente petición.**

En este código solo podríamos hacer una misma cosa al mismo tiempo. Si nuestra aplicación tuviera varias peticiones de este código al mismo tiempo, cada nueva petición tendría que esperar a la resolución de la anterior. Esta estructura es la óptima en las arquitecturas multi-hilo, pues podemos generar diferentes llamadas de forma paralela.

Pero *Javascript* solo se ejecuta en un hilo, por lo tanto si tenemos que gestionar varias peticiones al mismo tiempo el código bloqueante ralentizaría mucho la correcta ejecución. Por ello usaremos código no bloqueante.

el flujo de un código no bloqueate sería:

1. **toma los datos.**

1. 
**entregalos a alguien.**

1. 
**ellos escribirán los datos en la base de datos.
**
1. 
**cuando terminen enviarán un mensaje de estado. 
en base al mensaje de estado se realizarán las siguientes tareas necesarias.
**

1. 
**espera para la siguiente petición.**


Lo que estamos haciendo en esta estructura es delegar todas las tareas que tengamos que realizar para así poder seguir recibiendo peticiones.

Un ejemplo en código de lo explicado anteriormente:



```javascript

//Código bloqueante:

    var synchronousPrint = function(){
		return “syncronous call”;
	};	
	
    //Código no bloqueante:
    var asynchronousPrint  = function(callback){
		callback(“asynchronous call);
        };
```

imprimir los resultados por pantalla de de estos dos métodos sería de la siguiente forma:

```javascript

	//impresión sincrona:
	console.log(synchronousPrint);

	>>salida: syncronous call

	//impresión asincrona:
	asynchronousPrint(function(value){
		console.log(value);
};

	>>salida: asynchronous call.
```
	
En la primera ejecución nos encontramos frente a una llamada llamada a la función y un valor de retorno cuando esta finalice las tareas designadas. Algo muy similar a lo encontrado en otros lenguajes como *Java*, *Python*, etc.

En cambio en la segunda función lo que estamos haciendo es llamar a la misma y cuando llega al punto que tiene que devolver algo, en puesto de retornarlo con valor, asignamos el valor generado como parámentro de la función. al haber declarado el parámetro de llamada como otra función esta nueva función tendrá como valor por defecto el valor generado por la primera y así podrá usarlo en el nuevo contexto, en este caso imprimir por pantalla. 

A simple vista puede parecer innecesario usar las funciones asincronas, pues al principio es más complejo de entender que el valor de retorno simple. Pero en *Javascript* no controlamos el flujo de ejecución, y de esta forma podremos generar una lógica lineal de forma que cuando se ejecute una tarea pase a la siguiente, y así sucesivamente hasta terminar con todos los callbacks.
Es muy común en *Javascript* encontrar códigos con este formato:

```javascript

	foo.save(function(err, fooVar){
		fooDao.delete(fooVar, function(info){
			fooDao.findById(fooVar.getId(),             
                                      function(fooVarFound){
				assert.isNull(fooVarFound, 'It should be null');
			});
		});
	});
```

Donde podemos ver cómo se realizan llamadas a métodos dentro de otros, y así hasta terminar con el flujo de la tarea esperada. Cuando dicho flujo consta de muchas llamadas a callbacks podemos caer en el llamado "infierno de los callbabacks", dando lugar a un código muy difícil de seguir. Para evitar esto hemos de dividir nuestra aplicación en diferentes módulos y subtareas, de forma que no implementemos la lógica dentro de una misma corriente.
