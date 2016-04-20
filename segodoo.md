este documento es de libre acceso y uso bajo los términos expuestos en la licencia: Atribución-CompartirIgual 3.0 Venezuela (CC BY-SA 3.0 VE), https://creativecommons.org/licenses/by-sa/3.0/ve/ se agrega una copia de la misma en este repositorio.

Documento referencial con fines didacticos elaborado por jorgescalona @jorgemustaine jorgescalona@riseup.net.
### Seguridad y control de acceso en odoo

El archivo ir.model.access.csv contiene derechos de acceso asosiados a un modelo, un grupo mediante un conjunto de permisos:

* id = identificador único de permisos (Ejemplo: MY_MODULE_res_partner_manager).
* name = nombre único para el permiso (Ejemplo: res_partner manager).
* model_id/id = nombre único de la clase donde lo deseas aplicar (Ejemplo: model_res_partner).
* group_id/id = grupo al que aplica la permisología (tu puedes definir en un xml o llamar a un grupo ya existente con la sintaxis module.group_id).
* perm_read,perm_write,perm_create,perm_unlink = son 4 valores para los permisos de lectura, escritura, creación e eliminación de registros donde 1 equivale al booleano True (es decir permite la acción).

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
### Enlaces de interes:

* [Seguridad en openerp](http://www.zbeanztech.com/blog/security-openerp)
* [Ejemplo de archivo ir.model.access.csv](https://github.com/OCA/OCB/blob/8.0/addons/crm_claim/security/ir.model.access.csv)
