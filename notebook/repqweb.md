Este documento es de libre acceso y uso bajo los términos expuestos en la licencia: Atribución-CompartirIgual 3.0 Venezuela (CC BY-SA 3.0 VE), https://creativecommons.org/licenses/by-sa/3.0/ve/ se agrega una copia de la misma en este repositorio.

Documento referencial con fines didacticos elaborado por jorgescalona @jorgemustaine jorgescalona@riseup.net.

### Reportes Qweb

Los reportes son escritos en HTML/QWeb, como una vista normal en Odoo, el renderizado en PDF es realizado por wkhtmltopdf que es una librería que renderiza HTML en PDF desde la línea de comandos:

`jorge@maq1:~/Desktop$wkhtmltopdf https://attakatara.wordpress.com/2015/12/26/domain-filter-odoo/ domainfilter.pdf`

El elemento <report> está disponible para definir un reporte:

```
<report
	id="report_sale_order"
    string="Quoatation / Order"
    model="sale.order"
    report_type="qweb-pdf"
    file="sale.report_saleorder"
    name="sale.report_saleorder"
/>

```
donde:

1. report_type (obligatorio)
	qweb-pdf
	qweb-html
1. groups
	Campo Many2many hacia los grupos que pueden ver/usar el reporte.
1. attachment_use
	Si se establece en True, se guardará como un archivo adjunto, puedes utilizar 	esta opción si necesita que su informe se genere sólo una vez.
1. attachment
	Expresión python que define el nombre de el reporte, el registro es accesible 	como la variable object.

Ejemplo:
```
<report
    id="account_invoices"
    model="account.invoice"
    string="Invoices"
    report_type="qweb-pdf"
    name="account.report_invoice"
    file="account.report_invoice"
    attachment_use="True"
    attachment="(object.state in ('open','paid')) and
        ('INV'+(object.number or '').replace('/','')+'.pdf')"
/>

```
### Formato de papel
Son registros del tipo: report.paperformat y puede contener los siguientes atributos:

* format
	Cualquiera de los formatos predefinidos (A0 to A9, B0 to B10, Legal, Letter, 	Tabloid,…) o custom; A4 por defecto
* dpi
	90 por defecto
* margin_top, margin_bottom, margin_left, margin_right
	Tamaño de márgenes en mm
* page_height, page_width
	Dimensión de la página en mm
* orientacion
	Landscape o Portrait
* header_line
	Booleano para mostrar una linea de cabecera
* header_spacing
	Espaciamiento de cabecera en mm

Ejemplo:

```
<record id="paperformat_frenchcheck" model="report.paperformat">
    <field name="name">French Bank Check</field>
    <field name="default" eval="True"/>
    <field name="format">custom</field>
    <field name="page_height">80</field>
    <field name="page_width">175</field>
    <field name="orientation">Portrait</field>
    <field name="margin_top">3</field>
    <field name="margin_bottom">3</field>
    <field name="margin_left">3</field>
    <field name="margin_right">3</field>
    <field name="header_line" eval="False"/>
    <field name="header_spacing">3</field>
    <field name="dpi">80</field>
</record>

```
### Perzonalizando Reportes:
Los modelos de reportes tienen una función por defecto: get_html que busca un modelo denominado: report.module.report_name, si existe se llamará al motor QWeb. Así también, existe una función genérica: render_html, donde ser puede pasar objetos en el diccionario docargs.

```
from openerp import api, models
 
class ParticularReport(models.AbstractModel):
    _name = 'report.module.report_name'
    @api.multi
    def render_html(self, data=None):
        report_obj = self.env['report']
        report = report_obj._get_report_from_name('module.report_name')
        docargs = {
            'doc_ids': self._ids,
            'doc_model': report.model,
            'docs': self,
        }
        return report_obj.render('module.report_name', docargs)

```
### notas:
* Los reportes son generados dinámicamente por el módulo report y puede ser accedido por URL.
* Cada reporte debe poseer un registro en `ir.actions.report.xml`
* elementos necesarios para poder crear el reporte:
1. un template `ir.ui.view` registro.
1. un registro de reporte `ir.actions.report.xml`
1. y opcionalmente una especificación del papel en `report.paperformat`

Estructura del módulo
-----------------------

Este modelo de reporte (estructura) puede tener 3 formas principales:
* get_html
* get_pdf
* get_action

get_html busca un modelo llamado: `report.<<report_name>>`. de existir get_html
returns `report.<<report_name>>.render_html()`. de no existir, get_html usará un  render_html genérico.

Está es la principal diferencia entre un genérico y un reporte particular.

Generic / particular report
===========================

Generic / particular report
---------------------------
* **Generic**
    * Renderización de contexto genérica (*docs*, *translate_doc*, ...)
* **Particular**
    * Renderización de contexto nueva, cualquier forma en la que tu desees procesar tu data.
    * Odoo AbstractModel, requiere de un módulo customizado a la medida.

Para un reporte particular tienes que ecribir un módulo Odoo que contenga el método ` render_html`. Por lo general este método retorna un llamado al **QWeb render** en un **custom rendering context**. 

Escribiendo un reporte particular
---------------------------------



    from openerp.osv import osv


    class ParticularReport(osv.AbstractModel):
        _name = 'report.<<module.reportname>>'
        def render_html(self, cr, uid, ids, data=None, context=None):
            report_obj = self.pool['report']
            report = report_obj._get_report_from_name(
                cr, uid, '<<module.reportname>>'
            )
            docargs = {
                'doc_ids': ids,
                'doc_model': report.model,
                'docs': self.pool[report.model].browse(
                    cr, uid, ids, context=context
                ),
            }
            return report_obj.render(
                cr, uid, ids, '<<module.reportname>>',
                docargs, context=context
            )



### Enlaces relacionados:

* [Documentación Oficial Odoo Reports](https://www.odoo.com/documentation/9.0/reference/reports.html)
* [Documentación Oficial en GitHub](https://github.com/odoo/odoodays-2014/blob/master/v8_reporting_engine/index.rst)
* [blog de coronado edgar reportes qweb](https://coronadoedgar.wordpress.com/2015/05/15/reportes-qweb/)
* [Formación Bachaco-VE vistas Kanban y Reportes](https://github.com/Bachaco-ve/formacion-bachaco/blob/master/capitulo_viii_qweb.md)
* [Github Oficial de wkhtmltopdf](https://github.com/wkhtmltopdf)
* [Vídeo Qweb Report Customisation Development](https://www.youtube.com/watch?v=tCAUm3MWYzk)








