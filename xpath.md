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

### Enlaces de intéres y relacionados:

* [XML Path Language Xpath 3.0](https://www.w3.org/TR/xpath-30/)
* [XQuery and Xpath Data Model 3.0](https://www.w3.org/TR/xpath-datamodel-30/)
* [XPath and XQuery Functions and Operators 3.0](https://www.w3.org/TR/xpath-functions-30/)




