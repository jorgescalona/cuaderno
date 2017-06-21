Estructura de un módulo RML
===========================

El lenguaje estructurado rml, además de muy parecido a xml es la forma de facto para generar reportes en Odoo.

El framework siempre nos dará la facilidad de heredar pero para la crecaión de los reportes desde cero es importanter entender la estructura usada por Odoo para organizar los archivos que indicaran la construcción del objeto y las instancias del informe(s) deseados.

La estructura base del árbol del reporte será entonces un directorio en la raíz del módulo, el mismo se llamará report y su estructura es similar a:

report
   |-`__init__.py`
   |- reporte.xml
   |- reporte.py
   |- reporte.rml

El archivo **`__init__.py`** debe contener algo similar a: `import reporte` 

** reporte.xml **:

```
<?xml version="1.0" encoding="utf-8"?>
<openerp>
    <data>
    
        <report
            id="imprimir_reporte"
            name="imprimir.reporte"
            model="tabla.estudiante"
            rml="app_modulo/report/reporte.rml"
            string="Reporte PDF"
        />
            
    </data>
</openerp>

```

** reporte.py **:

```
# -*- coding: utf-8 -*-

import time
from openerp.report import report_sxw

class impresion_reporte(report_sxw.rml_parse):
    def __init__(self, cr, uid, name, context):
        super(impresion_reporte, self).__init__(cr, uid, name, context=context)
        self.localcontext.update({
            'time': time
        })

report_sxw.report_sxw('report.albaranes.entrada.pre',
    'app_modulo/report/reporte.rml',
    parser=imprimir_reporte,
    header='external'
)

```

En este caso en el parámetro **header** se indicá el tipo de encabezado que tendrá el documento. el parámetro **parse** debe ser el mismo nombre del **id** del elemento report que se a creado en el archivo **reporte.xml**. 

**nota**: cuando hacemos clic sobre Reporte PDF mediante el **id** se llamará el método que montará los valores del archivo rml donde está construida nuestra estructura.

** reporte.rml **:

```
<?xml version="1.0" encoding="UTF-8"?>
<document filename="Reporte_Impreso.pdf">
  
  <template pageSize="(595.0,842.0)" title="Reporte Impreso" author="Satélite Guayana (@sateliteguayana)" allowSplitting="20">
    <pageTemplate id="first">
        <frame id="first" x1="0.0" y1="57.0" width="538" height="728"/>
    </pageTemplate>
  </template>
  
  <stylesheet>
  
    <blockTableStyle id="letters_tab">
        <blockAlignment value="LEFT"/>
        <blockValign value="TOP"/>
    </blockTableStyle>
  
    <blockTableStyle id="linea_tab_head">
        <blockAlignment value="LEFT"/>
        <blockValign value="TOP"/>
        <lineStyle kind="LINEBELOW" colorName="#000000" start="0,-1" stop="0,-1"/>
        <lineStyle kind="LINEBELOW" colorName="#000000" start="1,-1" stop="1,-1"/>
        <lineStyle kind="LINEBELOW" colorName="#000000" start="2,-1" stop="2,-1"/>
        <lineStyle kind="LINEBELOW" colorName="#000000" start="3,-1" stop="3,-1"/>
        <lineStyle kind="LINEBELOW" colorName="#000000" start="4,-1" stop="4,-1"/>
        <lineStyle kind="LINEBELOW" colorName="#000000" start="5,-1" stop="5,-1"/>
        <lineStyle kind="LINEBELOW" colorName="#000000" start="6,-1" stop="6,-1"/>
    </blockTableStyle>
    
    <blockTableStyle id="linea_tab_normal">
        <blockAlignment value="LEFT"/>
        <blockValign value="TOP"/>
        <lineStyle kind="LINEBEFORE" colorName="#e6e6e6" start="0,-1" stop="0,-1"/>
        <lineStyle kind="LINEBELOW" colorName="#e6e6e6" start="0,-1" stop="0,-1"/>
        <lineStyle kind="LINEAFTER" colorName="#e6e6e6" start="0,-1" stop="0,-1"/>
        <lineStyle kind="LINEBELOW" colorName="#e6e6e6" start="1,-1" stop="1,-1"/>
        <lineStyle kind="LINEAFTER" colorName="#e6e6e6" start="0,-1" stop="1,-1"/>
        <lineStyle kind="LINEBELOW" colorName="#e6e6e6" start="2,-1" stop="2,-1"/>
        <lineStyle kind="LINEAFTER" colorName="#e6e6e6" start="0,-1" stop="2,-1"/>
        <lineStyle kind="LINEBELOW" colorName="#e6e6e6" start="3,-1" stop="3,-1"/>
        <lineStyle kind="LINEAFTER" colorName="#e6e6e6" start="0,-1" stop="3,-1"/>
        <lineStyle kind="LINEBELOW" colorName="#e6e6e6" start="4,-1" stop="4,-1"/>
        <lineStyle kind="LINEAFTER" colorName="#e6e6e6" start="0,-1" stop="4,-1"/>
        <lineStyle kind="LINEBELOW" colorName="#e6e6e6" start="5,-1" stop="5,-1"/>
        <lineStyle kind="LINEAFTER" colorName="#e6e6e6" start="0,-1" stop="5,-1"/>
        <lineStyle kind="LINEBELOW" colorName="#e6e6e6" start="6,-1" stop="6,-1"/>
        <lineStyle kind="LINEAFTER" colorName="#e6e6e6" start="0,-1" stop="6,-1"/>
    </blockTableStyle>
    
    <initialize><paraStyle name="all" alignment="justify"/></initialize>
    <paraStyle name="modelo_8" fontName="Helvetica" fontSize="8.0" leading="10" alignment="LEFT" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="terp_default_Bold_8" fontName="Helvetica-Bold" fontSize="8.0" leading="10" alignment="LEFT" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="head_modelo" fontName="Helvetica-Bold" fontSize="8.0" leading="11" alignment="LEFT" spaceBefore="0.0" spaceAfter="0.0"/>    
    <paraStyle name="head_modelo_6" fontName="Helvetica-Bold" fontSize="6.0" leading="11" alignment="LEFT" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="head_modelo_Centre" fontName="Helvetica-Bold" fontSize="8.0" leading="11" alignment="CENTER" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="head_modelo_6_centro" fontName="Helvetica-Bold" fontSize="6.0" leading="11" alignment="CENTER" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="terp_default_Centre_8" fontName="Helvetica" fontSize="8.0" leading="10" alignment="CENTER" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="terp_default_Centre_9" fontName="Helvetica" fontSize="8.0" leading="11" alignment="CENTER" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="cont_modelo_6_centro" fontName="Helvetica" fontSize="6.0" leading="11" alignment="CENTER" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="linea_tab_head_1" fontName="Helvetica-Bold" fontSize="8.0" leading="10" alignment="LEFT" spaceBefore="6.0" spaceAfter="6.0"/>
    <paraStyle name="linea_tab_head_1_Centre" fontName="Helvetica-Bold" fontSize="8.0" leading="10" alignment="CENTER" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="linea_tab_head_1_Right" fontName="Helvetica-Bold" fontSize="8.0" leading="10" alignment="RIGHT" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="head_modelo_Right" fontName="Helvetica-Bold" fontSize="8.0" leading="11" alignment="RIGHT" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="cont_modelo_6_normal" fontName="Helvetica" fontSize="6.0" leading="11" alignment="LEFT" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="cont_modelo_6_bold" fontName="Helvetica-Bold" fontSize="6.0" leading="11" alignment="LEFT" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="cont_modelo_6_right" fontName="Helvetica" fontSize="6.0" leading="11" alignment="RIGHT" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="terp_default_2" fontName="Helvetica" fontSize="2.0" leading="3" alignment="LEFT" spaceBefore="0.0" spaceAfter="0.0"/>
    <paraStyle name="espacio_5cm" fontName="Helvetica" fontSize="8.0" leading="10" alignment="LEFT" spaceBefore="6.0" spaceAfter="0.0"/>
    <paraStyle name="espacio_1cm" fontName="Helvetica" fontSize="8.0" leading="10" alignment="LEFT" spaceBefore="3.0" spaceAfter="0.0"/>
    <images/>
  </stylesheet>
  
  <story>
  <pto>
    <para style="modelo_8">[[repeatIn(objects,'estudiante')]]</para>    
    <para style="espacio_1cm"><font color="white"> </font></para>        
    <blockTable style="letters_tab">
        <tr><td width="500"><para style="terp_header">Código de pre-entrada: [[ estudiante.name ]]</para></td></tr>
    </blockTable>    
    <para style="espacio_5cm"><font color="white"> </font></para>    
    <blockTable style="Header_Order_Reference_Tbl">
        <tr>
            <td width="100.0"><para style="linea_tab_head_1">Dirección</para></td>
            <td width="100.0"><para style="modelo_8">[[estudiante.direccion or '' ]]</para></td>
            <td width="100.0"><para style="linea_tab_head_1">Correo electrónico</para></td>
            <td width="100.0"><para style="modelo_8">[[ estudiante.email or '' ]]</para></td>
        </tr>
        <tr>
            <td width="100.0"><para style="linea_tab_head_1">Nivel</para></td>
            <td width="100.0"><para style="modelo_8">[[ estudiante.nivel or '' ]]</para></td>
            <td width="100.0"><para style="linea_tab_head_1">Turno</para></td>
            <td width="100.0"><para style="modelo_8">[[estudiante.turno_id.name or '' ]]</para></td>
        </tr>
    </blockTable>
    <blockTable repeatRows="1" style="linea_tab_head" colWidths="200.0,120.0,50.0,50.0,50.0">
        <tr>
            <td><para style="head_modelo">Materia</para></td>
            <td><para style="head_modelo">Sección</para></td>
            <td><para style="head_modelo_6_centro">Aula</para></td>
            <td><para style="head_modelo_6_centro">Hora</para></td>
            <td><para style="head_modelo_6_centro">Día</para></td>
        </tr>
    </blockTable>
    <section>
        <para style="terp_default_2">[[ repeatIn([line for line in estudiante.materias_ids],'materias') ]]</para>
        <blockTable style="linea_tab_normal" colWidths="200.0,120.0,50.0,50.0,50.0">
            <tr>
                <td><para style="cont_modelo_6_normal">[[ materias.name or '' ]]</para></td>
                <td><para style="cont_modelo_6_normal">[[ materias.seccion or '' ]]</para></td>
                <td><para style="cont_modelo_6_centro">[[ materias.aula_id.name or '' ]]</para></td>
                <td><para style="cont_modelo_6_centro">[[ materias.hora or '' ]]</para></td>
                <td><para style="cont_modelo_6_centro">[[ materias.dia or '' ]]</para></td>
            </tr>
        </blockTable>
    </section>
    
  </pto>
  </story>
</document>

```

La importancia de este archivo rml es que el mismo proporciona todo el formato o plantilla de como deben mostrarse los datos en el PDF. en la sección **template** se configuran los parámetros base del archivo, en **stylesheet** se configura el estilo y diseño de las tablas, fuentes columnas, alineación de los párrafos, entre otras caracteriśticas. Secciones **story** y **pto**, va el argumento del reporte o contenido real, donde se mostrarán los datos de la tabla que hemos definido en el atributo del archivo **reporte.xml**.

**En resumen**: el diseño y el contenido la plantilla se define con la etiqueta `<template></template>`,  el diseño con la etiqueta `<stylesheet> </stylesheet>` y el cuerpo con la etiqueta `<story></story>`

Para un resumén de etiquetas y estilo hacer clic [AQUí](https://xmeele.wordpress.com/2013/10/19/openerp-reportes/).





### Enlaces relacionados:

* [Creación de reportes rml en openerp odoo](https://sateliteguayana.wordpress.com/2015/04/29/creacion-de-reportes-con-rml-en-openerp-odoo/)
* [Blog que describe los parámetros del RML](https://xmeele.wordpress.com/2013/10/19/openerp-reportes/)