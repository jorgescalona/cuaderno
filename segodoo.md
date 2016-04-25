este documento es de libre acceso y uso bajo los términos expuestos en la licencia: Atribución-CompartirIgual 3.0 Venezuela (CC BY-SA 3.0 VE), https://creativecommons.org/licenses/by-sa/3.0/ve/ se agrega una copia de la misma en este repositorio.

Documento referencial con fines didacticos elaborado por jorgescalona @jorgemustaine jorgescalona@riseup.net.
### Seguridad y control de acceso en odoo

El archivo ir.model.access.csv contiene derechos de acceso asosiados a un modelo, un grupo mediante un conjunto de permisos:

* id = identificador único de permisos (Ejemplo: MY_MODULE_res_partner_manager).
* name = nombre único para el permiso (Ejemplo: res_partner manager).
* model_id/id = nombre único de la clase donde lo deseas aplicar (Ejemplo: model_res_partner).
* group_id/id = grupo al que aplica la permisología (tu puedes definir en un xml o llamar a un grupo ya existente con la sintaxis module.group_id).
* perm_read,perm_write,perm_create,perm_unlink = son 4 valores para los permisos de lectura, escritura, creación e eliminación de registros donde 1 equivale al booleano True (es decir permite la acción).

Los usuarios y sus passwords son almacenados en la tabla res_users. (para entender mejor la creación de usuarios revisar res_users.py_), en el mismo nos percatamos que el manejo de las paswords se hace de forma transparente y sin encriptación por lo que se recomienda la instalación de un módulo de password encryption llamado "encrypt user password". Esto ultimo no se recomienda para despliegues en producción para estos ultimos mejor usar con LDAP. Otra forma es usar OpenID Authentification.
Los grupos pueden ser creados como registros en el modelo res.groups normales y los accesos al menú se pueden definir en las definiciones del menú.

```
<record id="group_cp_user" model="res.groups">
	<field name="name"> cp Administradores / Managers </field>
</record>

<record model='ir.ui.menu' id='menu_cp_algo'>
	<field name="groups_id" eval="[(6.0,[ref('group_cp_user')])]" />
</record>

```

Menu access definition

```
<menuitem "submenu_cp_user" name="cp administración" action="action_cp_user" parent="file_menu_config" groups="group_cp_user" />

```
### Niveles de seguridad en OpenERP

* Nivel SO:
 Los servicios deben correr como usuario y no como root:
 
1.  Servidor OpenERP -- openerp openerp
1.  PostgreSQL -- postgres / postgres
1.  Apache / ngix -- www-data / www-data

* Nivel PostgreSQL:

1. Dos tipos de usuarios: administrador y no administrador 
1. Dos roles para una bd: owner, otros ....
1. Control usando ACL.
1. Protocolos de autentificación pg_hba_.conf.
1.1 Socket IP (PG-md5).
1.2 Socket Unix (PAM- peer).

* Nivel OpenERP:

1. Modelos: res_users / res_groups
1. Autentificación: local, LDAP, OpenID, OAuth
1. Listas de acceso: que permiso tiene un grupo para un objeto.
1. Injection code: Controlado Frontend/Cliente - BackEnd/Servidor.
1.1 Dominions:[('name','=','Cristian')]
1. Nivel Menues 
1. Nivel Vistas
1. Carpeta Security
    * security.xml: res.group, ir.rules
    * ir.model.access.csv: CSV con reglas de acceso.
1. Funciones de Objetos:
    * def f(self, cr, uid, ids, ... context=None, ...)
    * cr: cursor de la bd.
    * uid: User ID.
    * ids: Instancias del objeto.

nota: importante recordar incluir los archivos security.xml en el descriptor del módulo _____openerp__.py en la sección update.

### Enlaces de interes:

* [Seguridad en openerp](http://www.zbeanztech.com/blog/security-openerp)
* [Ejemplo de archivo ir.model.access.csv](https://github.com/OCA/OCB/blob/8.0/addons/crm_claim/security/ir.model.access.csv)
* [vídeo sobre seguridad en OpenERP](https://www.youtube.com/watch?v=KeUUARKSVuE)

