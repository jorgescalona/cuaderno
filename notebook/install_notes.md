# Notas varias de instalación
## y preparación de ambiente (enviroment) de desarrollo

### docker-ce

* Docker usa aufs (union filesystem) para crear tanto los layouts como los puntos de montaje (mnt).
* Docker usa dkms framework para agregar modulos de kernel y permitir la comunicación con el mismo.
* Una vez instalado docker sobre debian es necesario agregar el $USER al grupo docker y cambiar los permisos del socket para permitir su uso con un usuario no **sudo** con:
> $sudo usermod -a -G docker $USER
> $sudo chmod 666 /var/run/docker.sock
* https://docs.docker.com/get-started/

### Limpiar el sistema de contenedores

> $docker system prune

**también se puede revisar los siguientes cuatro comandos:**

> $docker container prune -f
> $docker image prune -f
> $docker network prune -f
> $docker volume prune -f

### cambiar alguna variable interna de un contenedor en background

la opción -d en docker hace que el container se ejecute en background, puede darse la oportunidad que necesitemos modificar alguna variable interna del mismo y lo podemos hacer así:

> $docker exec -ti 9d7cebd75dcf /bin/bash

# Al instalar virtualenv en debian
### agregar ruta al path

> export PATH=$PATH:~/.local/bin/

### Una vez está corriendo postgresql en un contenedor gestionar bd desde el mismo

> $psql -U odoo

ref:

https://stackoverflow.com/questions/37694987/connecting-to-postgresql-in-a-docker-container-from-outside

### Usando t2d

agregar a bashrc el alias correspondiente:

> alias t2d='travisfile2dockerfile --root-path=${HOME}/.t2d'

hacer pull de la imagen base:

> docker pull vauxoo/odoo-80-image-shippable-auto

Por ultimo clonar un proyecto el mismo debe incluir su respectivo .travis.yml

> t2d git@github.com:Vauxoo/forecast.git 8.0

ref:

**https://github.com/Vauxoo/travis2docker**

### OCA guidelines & Documentation

**https://github.com/OCA/maintainer-tools/blob/master/CONTRIBUTING.md**
**https://odoo-community.org/page/documentation**



### Guardando la Configuración de una Instancia de Odoo en un Archivo

http://pythonpiura.org/posts/guardando-la-configuracion-de-una-instancia-de-odoo-en-un-archivo/
