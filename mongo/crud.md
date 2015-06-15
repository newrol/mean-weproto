##Operaciones CRUD

Dentro de una base de datos llamada datos fooDatabase crearemos una serie de colecciónes, documentos y practicaremos algunas consultas sobre ellos.

###Insertar 

Insertaremos dos  nuevos documento dentro de la coleción fooCollection.

```javascript
	> db.fooCollection.insert({"name" : "antonia", "apellido" : "garcia"})
	>db.fooCollection.insert({"name" : "pepe", "apellido" : "Martinez"})

```

Al insertar el primer documento se creará la colección fooCollection y se insertará e documento, al insertar el segundo documento como la colección ya existe, simplemente se creará el nuevo registro.	

###Consultar

en lo referente a las consultas hay que tener claros una serie de conceptos:
		
* Se pueden lanzar consultas a la base de datos usando *find()* o *findOne()*.
		
* Se puede consular por condiciones.

* Las consultas devuelven un cursor a la base de datos, de forma que de forma perezosa va mostrando los documentos que el consultor necesita.
		 
* Una vez obtenido el cursor se pueden realizar toda clase de metaoperaciones sobre el cursor obtenido. 


Primero listaremos todos los documentos de la colección fooCollection:

```javascript
    >db.fooCollection.find()
```

A lo que se nos retornará algo parecido a esto:

```javascript
    { "_id" : ObjectId("556ecc27e00dd01ca454f03c"), "name" : "antonia", "apellido" : "garcia" }

    { "_id" : ObjectId("556ecc46e00dd01ca454f03d"), "name" : "pepe", "apellido" : "Martinez" }

```

Debemos recordar que el campo “_id” es la clave autogenerada por *mongoDB*.
	
Si al contrario usáramos el método *findOne()* por defecto se nos devolvería un 	cursor  con el primer documento de la colección. 

```javascript
    {
    	"_id" : ObjectId("556ecc27e00dd01ca454f03c"),
    	"name" : "antonia",
    	"apellido" : "garcia"
    }
```

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

```javascript
	>db.fooCollection.find({"name" : {"$eq" : "antonia"}})
```

Devolverá el cursor con el valor antonia:

```javascript

    { "_id" : ObjectId("556ecc27e00dd01ca454f03c"), "name" : "antonia", "apellido" : "garcia" }

```

varios condicionales pueden ser aplicados dentro del mismo find respentando la siguiente nomenclatura:

```javascript

    db.CollectionName.find({key : {$conditional 1 : “value”, $contdiitonal2 : “value” …}})
    
```

Podemos usar el operador $or Para lanzar consultas enlazadas:

```javascript
    db.fooCollection.find({"$or" : [{"name" : "pepe"},{"name" : "antonia"}]})

```


###Actualizar 

Para actualizar un documento primero hemos de lanzar la consulta que seleccione el valor que queremos cambiar y después tendremos 

```javascript
    db.CollectionName.update({key : {$condition : “value”},{new values in format "key" : value"}, { upsert: true })

```

Como podemos observar primero realizamos la consulta, después introducimos todos los valores que modificaremos y para terminar añadimos *upset :  true* para indicar que los cambios queden escritos, si no añadimos este único campo se nos imprimirá por pantalla una simulación de lo que ocurriría al aplicar el *update*

```javscript
    db.fooCollection.update({"name" : "pepe"},{"name" : "pepe", "apellido" : "nuevo"},{upsert : true})

```

Como se ha encontrado la condición de la consulta la consola nos devolverá la siguiente salida:

    WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

Donde se nos indica que se ha encontrado un valor coincidente y que uno de los valores se ha modificado.

###Eliminar

A la hora de realizar un borrado hemos de diferenciar entre borar una base de datos, borrar una colección o borrar uno o varios documentos.

* **borrar una base de datos:** nos situariamos dentro de la base de datos que deseamos borar y escribiríamos:
    
        db.dropDatabase()

*  **Borrar una colección:** nos situariamos dentro de la base de datos y escribiríamos

        db.drop_collection("Nombre de la coleción")
        
* **Borrar un documento:** Lanzaríamos una consulta pero en puesto de usar *find()* usaríamos *remove()*

        db.posts.remove({"name": "pepe"});