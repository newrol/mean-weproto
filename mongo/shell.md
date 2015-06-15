##Shell de mongoDB

Lo primero para poder acceder a *MongoDB* es tener nuestra instancia corriendo en el sistema, para ello hemos de tener el servicio *MongoDB* activo.

para acceder a una instancia local solo hemos de usar el comando:

	$mongo

Si en cambio queremos acceder a una instancia remota, y la configuración de esta nos lo permite,  el comando a ejecutar es 

	$mongo hostname:port/dbname

si quisieramos acceder a una instancia remota de mongo dentro del panel de control especifico de mongo sería:

	>conn = new Mongo(“hostname:port”)

	>db = conn.getDB(“dbName”)

Algunos comandos de administración útiles serían:

	>help para listar todas los comandos.
	
	>show dbs para listar todas las bases de datos de la instancia. 

	> use DBname para entrar a una base de datos, si esta no existe la crea.
	
	>show collections dentro de una bbdd lista las colecciones disponibles.

La consola de *mongoDB* puede iniciarse ejecutando un script pasado como parámetro cuando se llama al comando:

	$mongo scriptname.js

Desde dentro de la consola de *MongoDB* podríamos llamar al mismo script usando:

	>load(“scriptName.js”)
