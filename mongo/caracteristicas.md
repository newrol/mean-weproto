##Características 


mondoDB es orientada a documentos, en contra del modelo relacional. su esquema de funcionamiento básico es clave:valor. Este planteamiento hace que sea más intuitiva su conjunción con los lenguajes orientados a objetos o prototipos que con las bases de datos relacionales.

Además ha sido desarrollado para dividir el almacenamiento de datos en diferentes servidores cruzados compartiendo la misma lógica. En caso de necesitar más capacidad horizontal simplemente ha de añadirse una nueva instancia de mongoDB al cluster, es una idea muy parecida al cluster de node.js

Un resumen de las principales propiedades de mongoDB:

* El documento es la unidad basica de datos,el equivalente a una línea dentro del modelo relacional.

* La colección es el grupo de varios documentos con el mismo modelo, sería el equivalente a las tablas.

* una única instancia de mongoDB puede almacenar multitud de bases de datos independientes, cada una con sus diferentes colecciones.

* Todos los documentos tienen una clave especial “_id” que es única para esa colección (más adelante se entrará en detalle).

* MongoDB incluye en su instalación base una terminal de javascript para su administración y manipulación.

* Los datos que mongoDB almacena en disco se serializan en un formato llamado Bson, que prácticamente es lo mismo que un formato json, por lo tanto trabajaremos directamente con los mismo objetos entre javascript y mongoDB.
