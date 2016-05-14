Este documento es de libre acceso y uso bajo los términos expuestos en la licencia: Atribución-CompartirIgual 3.0 Venezuela (CC BY-SA 3.0 VE), https://creativecommons.org/licenses/by-sa/3.0/ve/ 
se agrega una copia de la misma en este repositorio.

Documento referencial con fines didácticos elaborado por jorgescalona @jorgemust
aine jorgescalona@riseup.net.


Buenas Prácticas en el desarrollo de Odoo
=========================================

A menudo cuando se programa suele suceder que finalicemos con un código bastante amplio lo que resulta en una dificil amnuntención del mismo. Para evitar estos inconvenientes es necesario obtener desde el principio buenas prácticas o técnicas para el desarrollo, no preocuparse por esto puede traer consecuencias tales como:

* No reconocer el código que nosotros mismos hemos construido.
* Dificultar la lectura por parte de terceros, lo que trae consigo dificultades para obtener soporte o poder legar el código a terceros.
* Hacer una actualización del core de Odoo y que nos dé un error con el --update=all. O que actualice pero que no tenga funcionalidad el módulo.

Ya Guido nos planteaba una dirección cuando explicaba que el código es leído con más frecuencia de lo que está escrito. Por lo tanto dedicar un tiempo a depurar las técnicas que nos permita tener un código legible es tan necesario como aprender a usar un sistema de control de versiones, lo que queremos decir es que existen una seria de habilidades previas que debemos pulir antes de iniciar a escribir código propiamente dicho. 

### Buenas Prácticas en la estructura del módulo

1. Carpeta **models** para los archivos .py
1. Carpeta **views** para las vistas.
1. Carpeta **reports** para los informes.
1. Carpeta **wizard** para los asistentes (vistas y códigos)
1. Carpeta **security** para la seguridad.
1. Otras carpetas son obligatorias: i18n, static
1. Un archivo para cada modelo

### A nivel de Campos:

1. Nombres y etiquetas en Inglés.
1. Descriptivos cortos.
1. Utilizar related, calculados, almacenados de forma adecuada.

### A nivel de Código:

1. Hacer imports relativos.
1. Nombres de clases CamelCase.
1. Nombres de métodos en minúsculas y con underscore como unión.
1. No sobreescribir métodos completos.
1. PEP8 (guía de estilos para código python)

### A nivel de Vistas:

1. No hacer nunca position = "replace".
1. Escoger bien detrás o delante de qué se coloca un elemento.
1. Deshacer cambios mínimos de interfaz (de posición, por ejemplo) convenciendo al cliente.
1. Evitar el xpath, cuando no se pueda hacerlo lo más relativo posible.

### A nivel testing:

1. Evita repetir errores.
1. Detecta errores que ni sabias que existian.
1. TDD (Test-Driven development), es una práctica de ingeniería de software que involucra otras dos prácticas: Escribir las pruebas primero (Test First Development) y Refactorización (Refactoring).

### Enlaces relacionados y de interés:
* [Buenas Prácticas en Odoo](https://odoospain.odoo.com/event/jornadas-odoo-2015-2015-06-15-2015-06-16-2/track/buenas-practicas-en-el-desarrollo-de-odoo-85)
* [PEP8](https://www.python.org/dev/peps/pep-0008/)
* [PEP8 en Español + PDF](http://recursospython.com/pep8es.pdf)
* [TDD](https://es.wikipedia.org/wiki/Desarrollo_guiado_por_pruebas)


