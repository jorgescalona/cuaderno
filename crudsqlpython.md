Este documento es de libre acceso y uso bajo los términos expuestos en la licencia: Atribución-CompartirIgual 3.0 Venezuela (CC BY-SA 3.0 VE), https://creativecommons.org/licenses/by-sa/3.0/ve/ se agrega una copia de la misma en este repositorio.

Documento referencial con fines didácticos elaborado por jorgescalona @jorgemustaine jorgescalona@riseup.net.

Crud + Sql, fácil en Python
===========================

Crud es un acrónimo inglés (Create, Read, Update and Delete) que al español seria: Crear, Leer, Actualizar y Borrar, y lo que describe son las operaciones básicas que se pueden hacer sobre una base de datos. Sql (Structure Query Language), es un lenguaje declarativo de acceso a bases de datos relacionales. 
Nuestro articulo versa sobre como realizar las operaciones crud con python. Para este caso usamos sqlite3 como sistema de gestión de base de datos relacional.
### Preparación del entorno python

Lo primero que debemos hacer es importar la libreria correspondiente con: `import sqlite3` (en el caso de postgresql seria `import pg`).
Luego se debe crear una conexión a la base de datos sobre la que actuaremos, ejemplo: `conn=sqlite3.connet('bd.sqlite')`, esto crea una instancia conn que llama al método connect de la libreria sqlite3.
Ahora necesitamos crear el cursor ejemplo: `cur=conn.cursor`, esto crea una nueva instancia cur que llama al método cursor, esto nos permite ejecutar sentencias sql desde python con la siguiente sintaxis: cur.execute(''' sentencia sql ''' ), una vez finalizadas las operaciones sobre la base de datos es necesario cerrar el socket abierto en la interacción con: cur.close().

### Operaciones crud

**Crear una tabla en la bd:**
`CREATE TABLE users(name VARCHAR(128), email VARCHAR(128))`
Crea una tabla user con los campos name y email del tipo varchar y de longitud 128 cada uno.

** Insertar registros en la bd:**
`INSERT INTO users(name,email) values('jorge','jorge@dominio')`
Inserta en la tabla users y los campos name y email los valores en la tupla values.

**Eliminar registros en la bd** 
`DELETE FROM users WHERE email='jorge@dominio'`
Elimina de la tabla user el registro coincidente con la expresión que le sigue a WHERE.

**Modificar registros de la bd:**
`UPDATE users SET name='pedro' WHERE email='jorge@dominio'`
actualiza la tabla user y sustituye el valor del campo name para el registro coincidente con la condición despues del WHERE.

### Ejemplos de scrpits en python que interactuan con bd sqlite:

```
import sqlite3

conn = sqlite3.connect('music.sqlite')
cur = conn.cursor()

cur.execute('DROP TABLE IF EXISTS Tracks ')
cur.execute('CREATE TABLE Tracks (title TEXT, plays INTEGER)')

conn.close()

```

En el script podemos ver que importa la librería para luego crear una conexión conn la base de datos music.sqlite, luego sirviendonos del cursor eliminamos la tabla tracks de existir con la instrucción sql DROP y luego crea la tabla Tracks, finaliza el script cerrando el socket, sencillo verdad :)

Un ejemplo más:

```
import sqlite3

conn = sqlite3.connect('music.sqlite')
cur = conn.cursor()

cur.execute('INSERT INTO Tracks (title, plays) VALUES ( ?, ? )', 
    ( 'Thunderstruck', 20 ) )
cur.execute('INSERT INTO Tracks (title, plays) VALUES ( ?, ? )', 
    ( 'My Way', 15 ) )
conn.commit()

print 'Tracks:'
cur.execute('SELECT title, plays FROM Tracks')
for row in cur :
     print row

cur.execute('DELETE FROM Tracks WHERE plays < 100')

cur.close()

```
Este ultimo inserta valores en la tabla Tracks y luego los lista haciendo uso de las sentencias sql INSERT y SELECT.




### Enlaces consultados:

[crud en wikipedia](https://es.wikipedia.org/wiki/CRUD)
[Sql en wikipedia](https://es.wikipedia.org/wiki/SQL)
[sqlite en wikipedia](https://es.wikipedia.org/wiki/SQLite)

### Enlaces recomendados:

[conexión y consultas a bds con python](http://librosweb.es/libro/python/capitulo_12/conectarse_a_la_base_de_datos_y_ejecutar_consultas.html)
[conexión a bds con python, postgres y mysql](http://www.python.org.ar/wiki/DbApi)

