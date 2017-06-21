

Ante todo reciban un cordial saludo a todos los co listeros, e estado leyendo los post y la verdad no queda más que sentirse complacido por la loable labor llevada a cabo tanto por los que publican como por aquellos que se toman su valioso tiempo en contestar haciendo del saber un bien universal.

El asunto es que con fines didacticos (autoformación, autoaprendizaje), estoy haciendo un módulo llamado cpsis [1] (adjunto repo en github).
Ahora mismo estoy intentando configurar un reporte perzonalizado qweb-pdf, para lo cual e investigado un poco tanto de fuentes oficiales como de particulares en la web, y e revisado algunos vídeos técnicos, pero la mayoría están orientados a la crecaión de reportes a través de la interfaz web del framework. Me e percatado de que la documentación existente no es muy explicita al respecto y me e propuesto a documentar mi investigación, para ello tengo un repo en GitHub [2] llamado cuaderno que trata sobre hojas sueltas de mis indagaciones personales a dispocición de todos y bajo licencia CC-BY, alli esta un markdown llamado repqweb.md [3] donde e resumido lo más resaltante de la investigación respecto a los reportes qweb en Odoo, así como enlaces de interes al respecto.

De lo aprendido hasta ahora entiendo que debemos poseer:

1. Archivo XML, este debe estar ubicado en yourModuleName/Views y por convención su nombre deberia ser report_name.xml (donde name es el nombre que escojas). En fin es un template en xml con la estructura del reporte.
1. Agregar el registro del reporte en un archivo XML cuyo nombre ModuleName_report.XML, para nuestro caso cpsis_report.xml, dentro del mismo la declaración del registro entre <record />
1. Informar al framework de la existencia del nuevo reporte modificando __openerp__.py y agregando report_cpsis.xml a la sección data.

Hasta aquí entiendo va todo bien. El asunto es que ya e configurado todo al respecto sin embargo no e podido generar el informe: uso debian y odoo v8.

Enlaces relacionados:

[1] https://github.com/jorgescalona/cpsis
[2] https://github.com/jorgescalona/cuaderno
[3] archivo __openerp__.py https://github.com/jorgescalona/cpsis/blob/testing/__openerp__.py
[4] archivo cpsis_report.xml https://github.com/jorgescalona/cpsis/blob/testing/cpsis_report.xml
[5] archivo cpinv_view.xml https://github.com/jorgescalona/cpsis/blob/testing/views/cpinv_view.xml
[6] archivo report_cp_inv.xml https://github.com/jorgescalona/cpsis/tree/testing/views

Sin embargo luego de actualizar lista de módulos y actualizar el módulo local instalado vemos en opciones instaladas en la sección Informes definidos: "este módulo no crea informes", como se ve en la siguiente figura:


Pregunta:

¿Algún tutorial que explique esto de manera más explicita?
¿Que me falta para que el framework considere mi custom report?


De antemano agradecido por sus respuestas y sugerencias 
