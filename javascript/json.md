##Json

Es un formato ligero para el intercambio de datos, es el subconjunto de la notación literal de objetos de *javaScript* y es una de las principales razones de que la pila *mean.js* funcione tan bien en conjunción.

El modelo *json* esta formado por agrupaciones de elementos clave : valor; donde el valor puede ser otro conjunto de clave valor.

*Json* es la serialización directa de los objetos de javascript, así como de mongo; que aunque en disco se guarde como bson, en la practica mantiene el mismo formato. Json también es usado para enviar datos a través de la red por lo tanto compite directamente con *xml* con la diferencia de que *json* es más intuitivo y más liviano. 

Al utilizar el formanto *json* en toda la pila de nuestra aplicación no será necesario preoucparnos de implementar "pasers", "wrappers" y demás modulos que son requeridos en otras arquitecturas para poder comunicar tecnologías con modelos de datos heterogéneos.
