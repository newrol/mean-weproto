##Operaciones CRUD

Dentro de una base de datos llamada datos fooDatabase crearemos una serie de colecciónes, documentos y practicaremos algunas consultas sobre ellos.

###Insertar documentos

Insertaremos dos  nuevos documento dentro de la coleción fooCollection.

		> db.fooCollection.insert({"name" : "antonia", "apellido" : "garcia"})
		>db.fooCollection.insert({"name" : "pepe", "apellido" : "Martinez"})


Al insertar el primer documento se creará la colección fooCollection y se insertará e documento, al insertar el segundo documento como la colección ya existe, simplemente se creará el nuevo registro.	

###Consultar documentos
	
en lo referente a las consultas hay que tener claros una serie de conceptos:
		
* Se pueden lanzar consutas a la base de datos usando find() o findOne().
		
* Se puede consular por condiciones.

* Las consultas devuelven un cursor a la base de datos, de forma que de forma perezosa va mostrando los documentos que el consultor necesita.
		 
* Una vez obtenido el cursor se pueden realizar toda clase de metaoperaciones sobre el cursor obtenido. 


Primero listaremos todos los documentos de la colección fooCollection:

		>db.fooCollection.find()

A lo que se nos returnará algo parecido a esto:

    { "_id" : ObjectId("556ecc27e00dd01ca454f03c"), "name" : "antonia", "apellido" : "garcia" }

    { "_id" : ObjectId("556ecc46e00dd01ca454f03d"), "name" : "pepe", "apellido" : "Martinez" }

Debemos recordar que el campo “_id” es la clave autogenerada por mongoDB.
	
Si al contrario usáramos el método findOne() por defecto se nos devolvería un 	cursor  con el primer documento de la colección. 

    {
    	"_id" : ObjectId("556ecc27e00dd01ca454f03c"),
    	"name" : "antonia",
    	"apellido" : "garcia"
    }

Al hacer una consulta podemos especificar una serie de condicionales 
realizarla.  Estos condicionales son:

* $lt para reprensetar < 
* $lte para representar <=
* $gt para representar >
* $gte para representar >=
* $eq para representar igualdad
* $ne para representar no igualdad
* $not es un metacondicional que, usado junto a una condición aplica la opuesta.

Ejemplo:

		>db.fooCollection.find({"name" : {"$eq" : "antonia"}})

Devolverá el cursor con el valor antonia:

    { "_id" : ObjectId("556ecc27e00dd01ca454f03c"), "name" : "antonia", "apellido" : "garcia" }

varios condicionales pueden ser aplicados dentro del mismo find respentando la siguiente nomenclatura:

    db.CollectionName.find({key : {$conditional 1 : “value”, $contdiitonal2 : “value” …}})
	

Podemos usar el operador $or Para lanzar consultas enlazadas:


