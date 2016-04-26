
Este documento es de libre acceso y uso bajo los términos expuestos en la licencia: Atribución-CompartirIgual 3.0 Venezuela (CC BY-SA 3.0 VE), https://creativecommons.org/licenses/by-sa/3.0/ve/ se agrega una copia de la misma en este repositorio.

Documento referencial con fines didacticos elaborado por jorgescalona @jorgemustaine jorgescalona@riseup.net.

# Documentación de la experiencia durante el aprendizaje de docker

Ante todo es importante diferenciar entre contenedor, imagen e instancias de contenedores, cada uno
de ellos usa un ID distinto, por lo que debe ser cuidadoso en este aspecto.

### Listar imagenes

> $docker images

### Listar contenedores en ejecución

> $docker ps 

### Listar todos los contenedores

> $docker ps -a


### Eliminar Contenedores

> $docker rm IDcontenedor

### Eliminar imagen

> $docker rmi IDimage

### hacer attach de un contenedor

> $docker attach IDcontainer

### Ejecutar imagen abrir seudo tty 

> docker run -t -i imagen /bin/bash

### Preparando el entorno para Odoo
crear las siguientes carpetas
* mkdir odooVx (donde Vx corresponde a la version de odoo)
* cd odooVx
* mkdir config
* mkdir sources
* mkdir postgresql
* chmod 777 -R config/ sources/

ahora levantamos postgres y odoo adaptado a este entorno 
> $docker run -p 5436:5432 -d -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -v ~/odooVx/postgresql:/var/lib/postgresql/data --restart=always --name db postgres

> $docker run -p 8069:8069 -p 8022:22 -v ~/odoo/odooVx/config:/etc/odoo -v ~/odooVx/sources:/mnt/extra-addons --name odoo --link db:db -t odoo 

Las carpetas config se guardaran las configuraciones y en sources nuestros addons

Al levantar con --restart=always docker se encarga de mantener siempre los servicios arriba, si reinicias el servidor los servicios se leventan solos

### iniciar el servicio en modo interactivo 

reemplazamos el -d por -ti -u root y agregando /bin/bash al final y borrando el --restart=always, es decir:

> docker run -ti -u root --link db:db -p 127.0.0.1:8069:8069 -p 8022:22 -v ~/odooVx/config:/etc/odoo -v ~/odooVx/sources:/mnt/extra-addons -v ~/odooVx/data_dir:/var/lib/odoo --name odoo /bin/bash

Luego correr odoo con:
>runuser -u odoo openerp-server -- -c /etc/odoo/openerp-server.conf


Enlaces de interes y que use para aprender sobre docker
=======================================================

* [Instalación y Primeros Pasos con Docker](http://www.cristalab.com/tutoriales/instalacion-y-primeros-pasos-en-docker-c114081l/)
* [Docker en debian x Ernesto Crespo](http://blog.crespo.org.ve/2015/12/uso-de-docker-en-debian-jessie-parte-1.html)
* [configurar el contenedor de odoo v9](https://github.com/docker-library/docs/tree/master/odoo)
* [Odoo Development Essentials Book traducción de BachacoVE](http://fundamentos-de-desarrollo-en-odoo.readthedocs.org/es/latest/index.html)
* [Odoo Argentina buen post sobre dockerizacion](http://www.odooargentina.com/page/instalar-usando-docker)
* [Vídeo odoo en 7 pasos con Docker](https://www.youtube.com/watch?v=sAHRqCWb5uU)


