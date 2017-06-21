Inmersión Docker
================

En docker se pueden crear imagenes de contenedores en dos modalidades **detach** e **interactive**, **detach** ejecutará el progama en segundo plano (background), esto simplemente arrancara el programa pero el mismo no será capturado (attach), en tu terminal, esto es perfecto para servicios y daemons que son programas que interactuan con otros programas a través de la red o a través de otras herramientas de comunicación (sockets por ejemplo), cuando queremos este tipo de programas corriendo en un contenedor debemos usar la opción: --detach o su forma corta -d, ejemplo: $docker run -d --name container_name. **Interactive** ejecutará el contenedor de manera que podamos interactuar con el mismo un ejemplo de correr un contenedor de este tipo seria: $docker run --interactive --tty --link web:web --name prueba_inter nombre_contenedor: /bin/bash  En este comando hemos ussado dos banderas con el comando run: **--interactive** y **--tty** la primera le dice a docker que mantenga la standard input (stdin) abierta para el contenedor si no se a capturado (attach) un terminal y la segunda **--tty** opción le dice a docker que situe una terminal virtual para este contenedor, lo cual nos permite pasar señales al contenedor, por lo general esto se estila cuando tienes un programa que interactua del tipo cli. En este caso estamos corriendo un programe de consola shell llamado **sh** pero se puede correr cualquier otro programa disponible dentro del contenedor. Una tecera forma de ejecutar un contenedor es de manera interactiva en este caso el programa dockerizado tratará con programas que ya corren de forma **detach** a través de la bandera (flag) **--link** durante la ejecución del run, comunmente este tipo de programas son conocidos como clientes u agentes.


### Corriendo contenedores interactivos

Muchas veces podemos necesitar ingresar a un contenedor de forma interactiva lo cual podemos hacer mediante el comando docker run y ejecutando algún servicio en el contenedor del tipo cli en el siguiente ejemplo se inicia un shell de comandos sh:

> docker run -t -i image /bin/bash

> docker run --interactive --tty --link odoo:odoo --name odoo_sh busybox:latest /bin/sh

### Docker LOGS

> docker log container_id

Debe mostrar un registro de las operaciones de dicho contenedor un historial de ejecución lo que nos puede servir para solucionar problemas puntuales aunque no es recomendable para un monitoreo detallado y/o prolongado.

### docker exec

este comando docker ejecuta un comando adicional dentro de un contenedor, claro está previamente el mismo debe haber arrancado. Ejemplo:

> docker exec container ps

En este caso el comando llama a ps el cual muestra todos los procesos corriendo en el contenedor con su respectivo PID.

### Posibles conflictos entre aplicaciones y/o contenedores:

* Dos programas quieren unirse al mismo puerto.
* Dos programas utilizan el mismo archivo temporal y el bloqueo de archivos lo impide.
* Dos programas utilizan diferentes versiones de bibliotecas (librerias) instaladas a nivel global.
* Dos copias del mismo programa quieren usar el mismo PID.
* Un segundo programa que ha instalado modifica una variable de entorno que otro programa utiliza ahora mismo y hace que el primero falle.

docker resuelve estos conflictos con namespace de linux, componentes virtualizados y otras herramientas que en conjunto permiten proporcionar un aislamiento a cada contenedor. Si no somos cuidadosos en la construcción de los sistemas podemos terminar creando metaconflictos o conflicto entre las docker layers.
Identificar los contenedores se puede complicar cuando el número de estos aumenta.

![granja de servidores web](/home/jorge/imagenes/websitefarm.png)

### la bandera o flag --cdifile

Esta es muy útil cuando queremos almacenar el cid hex-encoded de 1024bits generado por docker run o docker create durante la creacion de un contenedor, esto se convierte en una buena práctica que nos permitirá gestionar nuestra granja de contenedores, ejemplo:

> docker create --cdifile /tmp/container.cid image

obtener el cid del ultimo contenedor creado y truncado(los primeros 12 caracteres):

> docker ps -l -q

o bien:

> CID=$(docker ps --lastest --quiet)
> echo $CID

si desea el identificador no truncado use la bandera --no-trunc

Por **convención** los nombres de los contenedores deben ser un adjetivo personal de identificación seguido de underscore y un identificador de autoria ejemplos:

* nginx_jorge




