##Características 


Node.js incorpora varios "módulos básicos" compilados en el propio binario, que nos permiten realizar las tareas comunes para una aplicación web, los módulos por defecto  más importantes serían:
HTTP y Https: para gestionar las conexiones web.

* **OS:** para acceder al los elementos del sistema.

* **Crypto:** para cifrar datos.

* **IO:** para gestionar las entradas salidas de setreams, file streams y buffers

* **DNS:** para los nombres de dominio.

* **Socket:** para la gestión de sockets.

* **Process:** Para la gestión de procesos.


Un módulo que hemos de tener presente en entornos de producción es el módulo Cluster pues node solo se ejecuta en un núcleo y gracias a este módulo podremos hacer que nuestro hilo de ejecución se duplique aprovechando tantos nucleos como tengamos a nuestra disposición y queramos asignar a node. Esta capacidad hace de node un elemento fácil de escalar y nos permitirá rápidas previsiones de recursos a añadir en paralelo

Además y como se mostrará más adelante se podrán añadir infinidad de funcionalidades para cada tarea especifica que se requiera.