##Estrucutura

###Documentos

```javascript
    {  “nombre”  :  “foonombre”,  “apellido” : “fooApellido” }
```

La línea que se muestra arriba es un documento de mongoDB. Sus propiedades son nombre y apellido. Cada uno incluye sus correspondientes valores a su derecha.

dependiendo del valor de cada clave su tipo de dato será diferente, en mongoDB los tipos de datos son muy pareciedos a los de javascript:

* **null:** usado para representar que el valor es nulo y que al mismo tiempo no     
   existe….cosas de javascript…(usar solo en casos muy expecificos)

```javascript
    { “foo” : null  }
```

* **boolean:** valor booleano para expresar true o false.
		
```javascript
    { “foo” :  true }
```

* **number:** Valores del coma flotante de 64 bits.

```javascript
    { “foo” :  3 }, { “foo” : 5.12 }
```

	      //podríamos “forzar” a *MongoDB* a usar enteros de 32 bits con esta función:

		{“foo : NumberInt(“ 5”) }

* **String:** caracteres UTF8
		
	     	{ “foo” : “String que deseemos incluir” }

* **date:** Guarda los milisegundos pasados desde el 1 de enero de 1970 hasta el momento suministrado.

		{ “foo” : new Date() }


* **array:** Guarda una lista de valores
		
        { “foo” : [“x”, “y” , “z”] }

* **documentos embebidos:** Un documento puede poseer otro documento como propiedad:

		{ “foo” : {“foovar” : “var}}


* **Id de documento:** usado sobre todo para relaciones diferentes documentos entre si
	 	
		{ “foo” : objectId() }

Existen los datos binarios, código y expresiones regulares de javascript pero estos son menos usados.

Es conveniente tener en cuenta que una clave no puede obtener el caracter \0 pues es usado por mongoDB como valor significativo de final de la clave. Los valores . y $ tienen propiedades especiales por lo tanto solo se usarán cuando realicemos queries sobre la bbdd.

MongoDB es sensitivo al tipo y al caracter por lo tanto:

    { “foo” : 3 }               
	{“foo” : 3}

sería distitnto de:                     

	{“foo” : “3” }   
	{“Foo”: 3 }


un mismo documento de mongoDB no puede contener las mismas claves.
 
Cuando creamos un nuevo documento automáticamente se crea también el campo _id
Este campo es , para mongoDB, la clave principal de el documento. este campo está formado por 12 bytes que representados como una string nos muestran 24 dígitos hexadecimales, 2 dígitos por cada byte que almacenamos. Esto hace que mostrado por pantalla parezca una string pesada, pero en realidad es algo muy liviano generado a partir de la siguiente lógica.

	0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11
	[                ][       ][      ][           ]
	  timestamp        machine  pid      increment

Esta es la las de las claves de la escalabilidad de mongodb,  pues los id que generan son únicos para cada documento estén en la ejecución que se encuentren.


###Colecciones

Una colección en mongoDB representa un conjunto de documentos. En comparativa a una BBDD relacional podría decirse que es una tabla.

Una colección se identificará por su nombre; que ha de cumplir con las siguientes  normas gramáticales:

* no puede ser una String vacia (“”)

* no puede contener el caracter \0.

* no puede empezar con la palabra system, queda reservada para uso interno

* una colección creada por el usuario no puede contener el caracter$


Los documentos almacenados  una colección no tienen por qué seguir el mismo esquema de clave: valor

    { “foo” : “value” }

podría convivir en la misma colección que :

    {“fookey” : 1}

 
Que esta práctica esté permitida dentro de mongoDB no quiere decir que tenga que ser usada a la ligera, es más solo debería plantearse en distinguidas ocasiones. mantener cada tipo de documento en una colección diferente los aporta un esquema más sólido, además hace que las consultas que realicemos a esta colección aumenten su eficiencia. Es mucho más rápido obtener una lista de colecciones que una lista de todos los tipos de clave valor. 

dentro de mongoDB podemos tener subcolecciones como subdominio de una colección, lo cual nos permite una relación lógica entre nombres de colección. Podemos tener foocollection  con sus documentos dentro y crear foocollection.subfooCollection  con sus respectivos documentos dentro.

Al igual que usar diferentes esquemas documentos en una colección no está recomendado, usar subcolecciones es considerado como una buena práctica organizativa.




###Bases de datos

Son utilizadas para agrupar colecciones que funcionen bajo la misma aplicación. Como se comentó arriba una sola instancia de mongoDB puede contener infinidad de bases de datos.

Cada base de datos tiene sus propios permisos y cada base de datos se almacena en un fichero de disco diferente.

Al igual que las coleciones las bases de datos son identificadas por el nombre y están restringidas por las siguientes normas gramáticales.

* No puede ser una String vacia (“”)

* Cada caracter ha de ser ASCII.

* el nombre está limitado a 64 bytes.

los nombres de bases de datos “admin”, “local”, “config” están reservados por mongoDB.
