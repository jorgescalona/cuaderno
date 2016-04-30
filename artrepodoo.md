RML y QWeb motores básicos para la generación de reportes en Odoo
=================================================================

Luego de repasar la información que consegui en la web sobre reportes qweb en odoo me percate que la información localizada poco me ayudaba, así que decidi seguir indagando y escribir un articulo al respecto para mi blog http://www.attakatara.wordpress.com. La finalidad es exponer publicamente una guía para aquellos entusiastas de la programación y de está maravillosa herramienta llamada Odoo.

* ¿Como hacer simples cambios a las cabeceras y pie de páginas de tus reportes RML?
* La forma básica de como el framework de Odoo organiza los reportes y las formas.
* Como modificar y hacer cambios a los reportes usando el nuevo framework de Odoo8 y el lenguaje de templates QWeb.

Lo primero que debemos hacer es loguearnos como administrador en Odoo y comenzar a editar las cabeceras y pie de página, nos vamos a configuración y seleccionamos compañias modificamos la información general y luego pasamos a la pestaña Configuración de informes, allí podremos ver el XML que se usa para crear las plantillas para los reportes. Allí Odoo nos permitirá seleccionar el formato del papel y la fuente. Para quienes esten familiarizados con RML o XML este código será muy familiar.

### RML (Report Markup Language)

En versiones previas todos los documentos se construian mediante RML. Pero Odoo a evolucionado al nuevo lenguaje de plantillas QWeb, el cual es más común para plataformas moviles, websites y reportes sin embargo existen áreas para las cuales aún se utiliza RML tales como las cabeceras y pie de página.
RML es un lenguaje de marcas flexible creado por ReportLab Europe Ltd. Una de sus principales caracteristicas es que produce archivos del formato PDF. este formato de ADOBE es altamente aceptado, aparte de ser un formato abierto es aceptado en muchos paises. Odoo utiliza este formato como el principal método para el intercambio de información en documentos para usuario final.
RML provee la plantilla que Odoo necesita para producir los documentos. Modificando el RML podemos adaptar los reportes como más nos guste, para mayor información sobre RML consultar: http://www.reportlab.com/docs/rml2pdf-userguide.pdf

### Modificando cabeceras RML
En Odoo es posible hacer cambios sin modificar los documentos en si mismo, por ejemplo podemos cambiar las cabeceras y los pies de página de nuestros reportes.
Odoo expone la plantilla del reporte en configuración ya que es uno de los más frecuentes cambios requeridos. en el mismo existen tres segmentos que podemos modificar:
1. La plantilla para documentos que tipicamente es la que se verá externamente. Encabezado RML.
1. La plantilla para documentos y reportes que por lo general es la que se distribuye internamente. Encabezado interno RML.
1. La plantilla para documentos horizontales. Encabezado interno RML para informes apaisado.

Realizar los cambios sobre el RML es tan fácil como identificar la etiqueta correspondiente en nuestro caso `<!--page header -->` indica el encabezado,luego editarla ejemplo localizar `<drawString x="1.3cm" y="22.9cm">Mail:</drawString>`, en la siguiente línea `<drawRightString x="7cm" y="22.9cm">[[ company.partner_id.email or ''  ]]</drawRightString>`  modificar `[[ company.partner_id.email or ''  ]]` por el correo de tu compañia ya cambiaria esa referencia. hay que ser muy cuidadoso con los cambios alterar partes complejas del RML como por ejemplo `company.partner_id.email` pueden romper el renderizadfo de los reportes.
Lo mismo aplica para el pie de página solo que esta vez identificamos la etiqueta `<!-- page bottom-->`, realizamos con cuidado los cambios y guardamos.

### Entendiendo los campos dinámicos en los reportes

Cuando RML es procesado el texto que está entre corchetes `[[" and "]]`, es procesado de forma dinámica. Lo que quiere decir que el reporte no mostrará lo que textualmente está entre los corchetes sino que rellenará el mismo con información dsede el framework. Por ejemplo si el pie de página contiene `[[ user.name ]]` le dice al motor de reportes que lo sustituya por el valor de la referencia. Es bueno tomarse un tiempo en leer el RML e identificar este tipo de datos dinámicos.
Adicionalmente esta sintaxis puede ser usada para llamar métodos python, por ejemplo: `[[ display_address(company.partnert) ]]`.

### Como Odoo organiza los reportes

En la interfaz de Odoo y como administradores podemos dirigirnos a configuración/Técnico/informes/informes, lo que desplegará una ventana con información sobre los existentes, allí podemos ver información como el modelo asosiado al informe, el tipo de acción que dispará el reporte, la plantilla del mismo y el tipo de reporte.
Cada actualización de Odoo a traido consigo mejoras en el motor de informes, sin embargo aún soporta las caracteristicas más antiguas, pero todo apunta en la actualidad al uso de plantillas QWeb.

### QWeb framework

Adicionalmente al viejo formato RML la versión 8 trae consigo todo un nuevo framework dedicado a la materia de generación de informes lo que lo hace super más flexible hasta el punto de soportar dispositivos móviles. Un poderoso lenguaje de Templates llamado QWeb permite integrar la información desde Odoo para tus reportes. 

Las plantillas QWeb es el principal constructor actual tanto para CMS, sitios web y porsupuesto reportes, cuando se usa como CMS genera el código HTML correspondiente para informes funciona similar pero genera un PDF, la parte importante de todo esto es saber como modificar QWeb para obtener la habilidad de crear páginas dinámicas que se conectan directamente al framework de Odoo para generar las salidas deseadas.
La mejor forma de aprender es leer código ya hecho

### Tecnologias relacionadas:

* **Aeroo reports:** motor de reportes para Odoo basado en la libreria Aeroo. Las plantillas son creadas en ODF y fueron consideradas muy populares en Odoo7. https://apps.openerp.com/apps/modules/8.0/report_aeroo/
* **Jaspersoft reports:** ofrece una variedad de soluciones para reportes open source con un editor de forma gráfica. http://community.jaspersoft.com/project/jasperreports-server/releases
* **Ireport:** el software provee acceso y procesamiento de reportes para el diseño de reportes de manera gráfica. http://community.jaspersoft.com/project/ireport-designer
* **Pentaho/Kettle:** También conocido como Kettle es una herramienta muy usada para pasar formatos de reportes a excel u otros formatos. Si bien no posee la cantidad de herramientas de Jasper si tiene una muy robusta integración con Odoo. http://community.pentaho.com/projects/data-integration/

### Fuentes consultadas:

* [documentación oficial](https://www.odoo.com/documentation/8.0/reference/reports.html)
* [Configurando reportes QWeb en Odoo en vídeo](https://www.youtube.com/watch?v=1EnM1ZDnswM)
* [Libro "Working with Odoo" de Greg Moss](https://www.packtpub.com/big-data-and-business-intelligence/working-odoo)






