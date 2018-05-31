# Expresiones Regulares

Son patrones de texto mediantes los cuales se pueden optimizar actividades de busqueda y reconocimiento de segmentos de cadenas de caracteres en un archivo especifico o en un conjunto de ellos. Algunos ejemplos de lo que puede hacerse con re son cosas como:

* Comprobar o validar que una entrada en un formulario HTML sea una dirección de correo electrónico válida.
* Inspeccionar si un patrón de texto aparece en un archivo. esto puede ser l busqued de una palabra o un porción de la misma en un documento.
* Extraer porciones de texto de un documento. Ej: extraer el código postal de una dirección.
* Reemplazar partes de un texto. Ej: Cambiar "Azúl" por "Rojo" en un documento.

Como podemos apreciar la aplicabilidad es extensa pero la agilidad obtenida en l manipulación de grandes porciones de archivos es una compensación hasta adictiva para todos aquellos que pretendan automatizar tareas rutinarias, que de otra mnera serian tediosamente largas y en la práctica una sincera perdida de tiempo. Las re son independientes del lenguaje que se este usando.

### Antecedentes:

* Warren McCulloch and Walter Pitts NeuroFísicos publicaron  ["A logical calculus of the ideas immanent in nervous activity."](http://www.cs.cmu.edu/~./epxing/Class/10715/reading/McCulloch.and.Pitts.pdf) (1943). Este paper no solo representa el inicio de las re sino que también propone el primer modelo matemático para redes neuronales.
* Stephen Kleene, escribió el paper ["Representation of events in nerve nets and finite automata"](https://www.rand.org/content/dam/rand/pubs/research_memoranda/2008/RM704.pdf) (1956), donde acuñó los terminos __regular sets__ y __regular expressions__.
* Doce años después un ingeniero publica: ["Regular Expression Search Algorithm"](https://www.fing.edu.uy/inco/cursos/intropln/material/p419-thompson.pdf) Ken Thompson (1968), Ken es conocido por ser diseñador e implementador en UNIX del __lenguaje B__, el UTF-8, entre otros trabajos.
* El próximo hito importante fue la introducción de una biblioteca no propietaria de regex por Henry Spence y más tarde la creación del lenguaje de guiones PERL por Larry Wall. PERL agregó muchas modificaciones a la sintaxis de regex creando lo que se conoce como ["Perl Flavor"](https://perldoc.perl.org/perlre.html) o los sabores de perl. Muchas de las implementaciones posteriores en el resto de los lenguajes se basan en el perl flavor.
* la IEEE a través del estandar POSIX intentó un mejor soporte Unicode para regex esto se conoce como el ["POSIX flavor"](https://regular-expressions.mobi/posix.html?wlr=1).
* Ahora mismo python posee un módulo para regex que soporta el estilo perl [Documentación python regex module](https://pypi.python.org/pypi/regex). Además del ya archi conocido modulo estandar para [python2](https://docs.python.org/2/library/re.html) y [python3](https://docs.python.org/3/library/re.html).

### Definiciones:

Una Regex es un patrón de texto que consiste en caracteres ordinarios precedidos por __"/"__ y metcarateres precedidos por __"\"__.

___Metacaracteres:___
Caracteres con un significado especial para las búsquedas. Tienen un significado especial cuando se utilizan en una expresión de búsqueda.

___Comienzo y final de una línea:___ El __"^"__ (acento circunflejo) hace referencia al comienzo de la línea en una búsqueda y el __"$"__ (signo dólar) tiene referencia con el final de la línea.

> /^www/
> /$com/

__Comodines__: Regex tiene muchos aspectos heredados de [ed](https://es.wikipedia.org/wiki/Ed_(Unix) recordar cada uno de ellos se torna dificil, porque el significado de un simbolo depende de dónde se utilice en una expresión. Por ejemplo, en modo de entrada un punto __"."__ (punto) es simplemente un carácter ordinario de texto, salvo que se encuentre sólo en una línea, en cuyo caso significa "vuelve al modo orden". En modo orden, el __"."__ significa "cualquier carácter". Así, la orden:

>/a..b/

significa "encuentra una __a__ y una __b__ separadas por tres caracteres cualesquiera". La orden:

>/./

significa "encuentra cualquier carácter" (excepto un carácter de nueva-línea). Cuando el __"."__ punto aparece en el lado derecho de una expresión de sustitución, significa "un punto". Esto puede combinarse en una única orden:

>.s/././

Esta orden muestra todos los significados de un __"."__ en una expresión. El primer __"."__ significa "en la línea actual sustituya (para cualquier carácter) un punto (.)" por Ejemplo:

> p
> Buenos días
> s/././
> .uenos días

__El * (asterisco)__. "Tantas ocurrencias como ocurran incluyendo ninguna". Así la orden:

> s/xx*/y/

da instrucciones que en __ed__ sustituyen dos o más ocurrencias de __"x"__ por una única __"y"__. La orden:

> s/x.*y/Y

significa "sustituye el carácter Y por cualquier cadena que comience por una __"x"__ y finalice con una __"y"__ separadas por cualquier número de caracteres". Las cadenas __"xqwertyy", "xasdy" y "xy"__ serían sustituidas por __"Y"__.

___Recomendación:___ Todos estos ejemplos se pueden ejecutar desde el shell con la instrucción [__"sed"__](https://es.wikipedia.org/wiki/Sed_(inform%C3%A1tica) texto simple por ejemplo:

> sed -i 's/x.*y/Y/' ejemplo.txt

__El & (ampersand).__ el & es una abreviación que ahorra mucha escritura. Supongamos que se quiere cambiar:

> Este proyecto ha sido un éxito.

por

> (Este proyecto ha sido un éxito.)

Podría utilizar la orden

> s/Este proyecto ha sido un éxito./(Este proyecto ha sido un éxito.)/

Pero utilizando __"&"__ se simplifica a:

> s/Este proyecto ha sido un éxito./(&)/

__Clases de caracteres en la búsqueda:[]__ 

Se pueden especificar clases de cosas a buscar, para lo cual se usa __"[]"__ por ejemplo:

> [xy]

representa a la clase de letras minúsculas que son __"x"__ o __"z"__ de está forma:

> /[xz]/

buscará la siguiente __"x"__ o la siguiente __"z"__ de la expresión.

> [fF]

__"f"__ en minúsculas o mayúsculas, en consecuencia la orden de búsqueda:

> /[fF]reddy/

encontrará a "freddy" y "Freddy". La expresión:

> [0123456789]

buscará cualquier dígito, pero se puede simplicar con:

> [0-9]

que representá toodos los caracteres en el rango __"0"__ al __"9"__. La orden quedará:

> /[0-9]/

ahora:

> [A-Z]

representa todos los caracteres del rango de la __"A"__ a la __"Z"__. para definir un caracter que no se encuentr en está clase utilizar el __"^"__ circunflejo entre los corchetes __"[^]"__ lo cual representa cualquier carácter ___no___ incluido en los corchetes. la expresión siguiente:

> [^0-9]

representa cualquier carácter que no este entre __"0"__ y __"9"__; en otras palabras, cualquier carácter que no sea un dígito.


__caracteres especiales en Regex Tabla 1__


|__Carácter__|__Significado__|
|-----|----|
|__"."__|Cualquier carácter distinto de nueva línea.|
|__"*"__|Cero o más ocurreencias del caracter anterior.|
|__".*"__|Cero o más ocurrencias de cualquier carácter.|
|__"^"__|Comienzo de línea.|
|__"$"__|Final de línea.|
|__"[--]"__|Identifica a la clase de caracteres definida entre corchetes.|
|__"[^--]"__|Identifica a cualquier carácter no incluido en la clase definida entre corchetes.|
|__"\"__|Caraćter de escape; trata al siguiente carácter, __"X"__ como una X literal|

__Desactivación de caracteres especiales:__

Los caracteres __$ [] *__ son parte de la sintaxis de las Regex, todos tienen un significado especial en las búsquedas. Vea la Tabla 1. Ahora bien ¿qué pasa si queremos buscar uno de esos caracteres en un archivo? ¿qué ocurre si se necesita encontrar el __"$"__ en una memoria? El carácter __"\"__ Backslash se utiliza par desactivar ese significado especial de los metacaracteres. __Un metacarácter precedido de un \ significá el carácter literal__. Si usted teclea:

> / . /

el interprete buscaría cualquier carácter, la siguiente orden, sin embargo:

> / \ . /

busca un punto __"."__ literalmente y no cualquier carácter. La siguiente orden:

> / \ * /

busca un * literalmente. Y por supuesto:

> / \ \ /

busca un __"\"__ Backslash literal. y

> / \ $ /

busca un __"$"__


Estos patrones de busqueda pueden ser usados de distintas formas uno de los usos que particularmente le doy es con grep (dato curioso el nombre de este comando viene de la forma que tiene el editor __ed__ para las busquedas __g/re/p__ o __global/regular expression/print__), que es una utilidad de UNIX para desde la shell ubicar una línea en un archivo específico que coincida con un patrón un ejemplo sería:

> grep -InRi '^[mM]*ay' mbox.txt
> 54165:May have missed an end tag

en el anterior obtengo una lista númerada de las líneas dentro del archivo mbox.txt que coinciden con la expresión regular entre comillas simples. Espero que ya te estes percatando del poder de las Regex. Otra buena idea es usar guiones (scripts) para __sed o ed__, con lo cual podemos realizar tareas super rápidas de modificación sobre archivos si quieres profundizar sobre el tema recomiendo el siguiente [enlace](https://www.americati.com/doc/sed/sed.html).

### Python

Las regex son soportadas por el módulo __re__ una vez importado el mismo podemos comenzar a comparar patrones para hacerlo es necesario transformar un patron a __bytecode__, el bytecode puede ser luego ejecutado por un motor en C por lo tanto es un lenguaje intermedio o pasarela.

> patron = re.compile(r'\bfoo\b')
> patron.match("foo bar")

## Backslash en cadenas literales y python

Las Regex no forman parte del core de python, el Backslash se usa en regex para indicar el uso de un metacaracter, pero el mismo es usado en python para el uso de caracteres especiales esto trae consigo un pequeño inconveniente, supongamos que deseamos hacer coincidir un patron especifico para encontrar el caracter '\' en una cadena especifica supondria entonces un dilema interpretativo lo cual python resuelve usando __"\\"__ pero a la larga las expresiones se haran más larga y confusas un ejemplo de ello sería:

> patron = re.compile('\\\\\\\')
> patron.match("\\\\\\\\author")
<_sre.SRE_Match at 0x104a88e68>

Para evitar que la nomenclatura se haga más complicada python asume el raw string de la siguiente manera:

> pattern = re.compile(r"\\")
> pattern.match(r"\author")
<_sre.SRE_Match at 0x104a88f38>

___En Python existen dos tipos de objetos regex:__
* RegexObject:  también conocido como _Objeto Patrón_.
* MatchObject: Representa el patrón de coincidencia.

### Referencias

* [UNIX Sistema V Versión 4 2da Edición](https://www.amazon.com.mx/Unix-System-Release-Richard-Rosinski/dp/0078821304) Kenneth H. Rosen, Richard R. Rosinski, James M. Farber, Douglas A. Host. Editorial McGrawHill (1997).


