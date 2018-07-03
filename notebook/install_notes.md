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

### PIPENV deploy example

Sobre las ventajas de la nueva forma de despliegue de enviroments en Python [pipenv](https://realpython.com/pipenv-guide/ "PipEnv") sobre virtualenv por ejemplo

### Corriendo e instalando un nuevo modulo de odoo

> $/home/odoo/odoo-10.0/odoo-bin -d openerp_test -c /home/odoo/odoo-10.0/myodoo.cfg -i openacademy

#  V2

**Para crear el contenedor a partir de la imagen shippeable de Vauxoo:**

>$docker run -itP -e LANG=C.UTF-8 --entrypoint=tmux -v $HOME/.ssh/:/home/odoo/.ssh/ --name odoo-v10-0.2 e05e703818e9

**Una vez en el contenedor:**

>$whoami
>>> root
>$apt-get update && apt-get upgrade
>$apt-get install -y node-less node-clean-css xfonts-75dpi aptitude
>$git config --global user.name "Your Name"
>$git config --global user.email youremail@example.com

**ubicado en /home/odoo hacer:**

>$git clone -b 11.0 --single-branch https://github.com/odoo/odoo.git

>$su odoo %% cd /home/odoo/odoo
>$pip install -r requeriments.txt
>$npm install -g less less-plugin-clean-css
>$python odoo-bin -d odoo_test --db-filter=odoo_test

### Notas importantes sobre la instalación:

* La imagen shippeable de vauxoo ya tiene todo lo necesario y hasta los virtualenv de python y node, intentar correr un venv adicional es una inception.

### Generando ssh keys

* ssh-keygen -t rsa -C "escajorge@gmail.com.com"
