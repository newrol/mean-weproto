##Banco de trabajo


###### *"Un mal plan es mejor que no tener ningún plan." Frank Marshall, ajedrecista Estado Unidense”*


Aunque no es propósito directo de este escrito tratar elementos ajenos al desarrollo directo de nuestra idea, si considero correcto mostrar  someramente algunas buenas prácticas iniciales para  que en el momento de empezar a escribir nuestra aplicación el proceso sea eficiente y totalmente articulado.

1. 
**Implementar un buen control de versiones:** es decir git; es decir github o bitbucket. nada de códigos en memorias de usb, nada de mails con las últimas versiones, nada de cientos de carpetas en dropbox con las diferentes versiones del producto. Al utilizar nuestra aplicación con git como base tendremos la certeza de conocer el estado de nuestro código en todo momento y poder volver atrás, ramificar su desarrollo y conseguir esa agilidad buscada. Otro plus de usar git es que la mayoría de sandbox en la nube para ejecutar nuestro servidor se basan en él para desplegar la aplicación

1. 
**Entornos de desarrollo virtualizados:** No todos los desarrolladores usamos los mismos sistemas operativos, tener el servidor en desarrollo ejecutándose en local no es buena idea cuando otros usuarios han de testear nuestro código etc. Lo mejor es tener una máquina sirviendo máquinas virtuales laboratorio a los distintos desarrolladores. Para esta tarea recomiendo usar xen si disponemos hardware local o micro instancias en amazon aws si por el contrario no disponemos de dicho hardware.

1. 
**Integración continua:** Al trabajar varios programadores sobre el mismo código es buena práctica utilizar herramientas que nos ayuden a mantener la intregridad de nuestro código, y travis, en este caso es una opción a tener muy en cuenta con el construiremos de forma automatizada y continua nuestro proyecto así cuando se realicen cambios podremos testear que estas modificiaciones respetan la integridad base de nuestro proyecto.

1. 
**Disponer de un gestor de proyectos:** Con ello nuestro equipo podrá comunicarse de forma eficiente y tener un conocimiento general de todo el desarrollo, dentro de nuestro gestor se tratarán los diferentes bugs de nuestra aplicación los tiquets que se van abriendo etc. Jira es una opción muy consolidada para este fin.

1. 
**El IDE:** el entorno directo donde machacaremos las horas. ha de ser intuitivo y cumplir su tarea de agilizador y no un trasto pesado que esconde tareas básicas en submenus que requieren 15 clicks para llegar a la ansiada opción. Javascript no requiere de IDES pesados para funcionar. Con una herramienta estilo sublime text sería suficiente. Si nos sentimos cómodos en netbeans también sería una buena opción. Existen en el mercado alternativas propietarias con bastante renombre como webstorm. El IDE es algo muy personal y cada desarrollador tiene sus requerimientos  particulares, recomiendo elegir el que mejor se adapte a ellos.



No es objetivo de de este documento mostrar la instalación y despliegue de cada una de las tecnologías usadas, solo mostrar una introducción a cada una de las mismas, para que más tarde el desarrollador sea capaz de, con esta base, ir profundizando en cada una de ellas en referencia a sus necesidades. Por lo tanto, no se encontrará aquí documentación de este estilo. Cabe decir que todas las tecnologías mostradas tienen una web oficial con su correspondiente apartado de instalación. Donde podremos elegir la opción de despliegue que más se adapte a nuestras necesidades; paquetes de instalación personalizados para cada sistema operativo, sources fuentes (todo es software libre) para una eficiente instalación en entornos de producción etc.  

Ahora que disponemos de una base sólida sobre la que consolidar el desarrollo de nuestra aplicación comencemos.
