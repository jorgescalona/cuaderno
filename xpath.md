Este documento es de libre acceso y uso bajo los términos expuestos en la licencia: Atribución-CompartirIgual 3.0 Venezuela (CC BY-SA 3.0 VE), https://creativecommons.org/licenses/by-sa/3.0/ve/ 
se agrega una copia de la misma en este repositorio.

Documento referencial con fines didácticos elaborado por jorgescalona @jorgemust
aine jorgescalona@riseup.net.
Xpath
=====

Xpath es un estandar para el lenguaje de path en XML. Existe desde hace más de 15 años y se conocen 3 versiones:

* Xpath 1.0, como una recomendación de W3C el 16 de Noviembre de 1999. Es muy básica con respecto a sus sucesoras, solo soportaba 4  tipos de datos: node, booleam, number, string y un compendio reducido de funciones pre construida para ser exactos solo 27.
* Xpath 2.0, como una recomendación de W3C el 23 de Enero de 2007. Se considera un gran avance se introdujo en está versión un sistema de tipado general que soportaba cerca de 50 tipos, nuevos operadores y una biblioteca de funciones integrada con más de 100 funciones. Se introduce el **concepto de secuencias**, todos los valores de uns expresión Xpath 2.0 es una secuencia. **Conjuntos de nodos** en la ver 1.0 fueron reemplazados con **Secuencias de nodos** en la ver 3.0.
* Xpath 3.0, como una recomendación de W3C el 8 de Abril de 2014. Introduce nuevos tipos, operadores y más de 200 funciones nuevas. El más significativo aporte de la versiuón es la recursividad de funciones pudiendo ahora una función ser pasada a otra como argumento o retornar una función. Y permite escribir funciones propias del desarrollador **inline functions**, o crear su propias librerias de funciones.

con Xpath es posible identificar partes del documento XML y también ejecutar computos sobre esa data.

### Expresiones (expresions)

es el principal bloque de construcción en Xpath, una expresión es un simple string de caracteres unicode hecho de palabras claves, simbolos y operadores.

### Secuencias (sequences) 

Son muy importantes en Xpath ya que cada expresión retorna una secuencia. Así una secuencia es una simple colección de items que pueden ir desde cero o más de ellos.
Una secuencia sin items o vacía se conoce como: secuencia vacía (empty sequence).
Una secuencia con un item simple es conocida como secuencia simple (singleton sequence).
a partir de Xpath 3.0 un item en una secuencia puede ser un nodo, un valor atómico (atomic value), o una función. De esta manera Xpath 3.0 define 7 tipos de nodos:

1. documento (document).
1. element.
1. attribute.
1. namespace.
1. procesing instruction.
1. comment.
1. text.

Un valor atómico es un valor permitido de un conjunto de valores para un tipo atómico en particular. Los tipos atómicos son todos los tipos que se derivan de forma directa o indirecta de **xs:anyAtomicType**.Como se especifica en el diagrama de herencia de tipos de datos para XML Schema 1.1:

![XML Schema 1.1](https://www.w3.org/TR/xmlschema11-2/type-hierarchy-201104.png)

La **función** es un nuevo tipo de item. En Xpath 2.0 un item en una secuencia solo podía ser un nodo o un valor atómico. En Xpath 3.0 puede ser un nodo, un valor atómico o una función.

### Ubicación de la ruta (path)

Ubicar rutas es Xpath es muy similar a usar la notación de path para archivos en el sistema de archivos que usemos y al igual que este ultimo tenemos rutas relativas y absolutas, donde una ruta absoluta siempre es evaluada desde la raiz del arbol "/" y una ruta relativa se referencia a un nodo en especifico. la raiz del documento "/" es el nivel más alto del XML y es el contenedor de todos los nodos que lo componen inclusive el mismo. Una ruta absoluta también puede empezar con: "//" (lo que se refiere a todos los subnodos de la raiz) lo que es distinto a "/" (se refiere a la raiz, todo el documento, incluyendo nodos, expresiones y/o funciones).
Una ruta relativa es siempre evaluada desde el contexto de un nodo. Ejemplo:

`office/employee/first_name[.='John']`

El nodo contextual en el que esta evaluada está expresión es 'company' que es la raiz del archivo company_1.xml, el elemento padre es 'office'. El elemento contextual puede cambiar durante la evaluación de la expresión como lo indica el caracter punto '.' en este caso es usado para indicar el nodo contextual 'first_name' de esta forma se compara el valor de este nodo con el string 'John'.

### Steps

Una ruta de path contiene uno o más steps. Un step está compuesto de:

1. una axis. Es la primera parte de una ubicación step la que determina la dirección a navegar con respecto de un nodo particular. Existen 13 diferentes axisas pertenecientes a dos grupos: **forward axis** (estás retornan en el mismo orden que se encuentran en el documento XML) o **reverse axis (retornan de forma inversa al documento XML). Se usa "::" para separar la axisa especifica del node test. **
1. un node test. Aparece inmediatamente despues de la axis y pueden ser de tres tipos: por nombre, por kind o por tipo.
1. Cero o más predicates.

`axis::node_test[predicate]`

`child::office[@location='Viena']`

Está ultima expresión selecciona desde el nodo contextual todos los elementos hijos de 'office' que tengan un atributo llamado 'location' que a su vez sea igual a 'Vienna'.

Algunas Forward Axis:

* child
* descendant
* attribute
* self
* desendant-or-self
* following-sibling
* following
* namespace

Algunas Reverse Axis:

* parent
* ancestor
* preceding-sibling
* preceding
* ancestor-or-self

Ejemplo:

`child::office`

Está expresión Xpath es una ruta relativa la cual selecciona todos los elementos hijos del nodo contextual 'office'.

**node test**

* by name:
    **office**
    Está expresión Xpath contiene un nombre de nodo 'office' el cual selecciona todos los elementos hijos (de ese nodo contextual en especifico). Por eso no se especifica axisa alguna. La axisa child es asumida por defecto y es por ello que el principal tipo de nodo es la axisa child.

    **@location**
    Esta expresión Xpath selecciona el atributo llamado 'location' del nodo contextual. la forma abreviada de la axisa 'attribute' es '@'.

* by kind:
    los kind que se pueden aplicar a un nodo son:
    * document-node()
    * element()
    * attribute()
    * schema-element()
    * schema-attribute()
    * processing-instruction()
    * comment()
    * text()
    * namespace-node()
    * node()
    
    Ejemplos:
    
    **//attribute()**
    Esta expresión Xpath selecciona todos los atributos nodales en el documento XML (independientemente del nombre o el tipo). El doble slash al principio de la expresión es la forma corta de la axisa 'descendant-or-self'.

    **//element()**
    Esta expresión Xpath selecciona todos los elementos del documento XML (independientemente del nombre o el tipo).

    **//***
    Esta Expresión Xpath es el equivalente del ejemplo anterior. En esta forma abreviada el comodín '*' es usado para denotar los elementos nodales.

* by type:
    Los tipos de nodos que pueden ser evaluados son cualquiera de los presentados en la tabla de built-in Schema datatypes (arriba expuesta), como también cualquier tipo definido por el usuario o tipos complejos. Ejemplo:

    **//element(*,xs:date)**
    El primer argumento de la función en esta expresión Xpath es el nombre del nodo y el segundo argumento es el tipo. El asterisco es usado en el primer argumento y denota 'cualquier nombre'. La expresión selecciona todos los elementos del documento XML (insistintamente del nombre de elemento) los cuales tengan como tipo 'xs:date'.

### Enlaces de intéres y relacionados:

* [XML Path Language Xpath 3.0](https://www.w3.org/TR/xpath-30/)
* [XQuery and Xpath Data Model 3.0](https://www.w3.org/TR/xpath-datamodel-30/)
* [XPath and XQuery Functions and Operators 3.0](https://www.w3.org/TR/xpath-functions-30/)




