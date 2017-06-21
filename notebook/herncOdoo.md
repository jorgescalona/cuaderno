Procesos de Herencia en Odoo
============================

Mezcla de clases y Herencia delegada

La herencia delegada permite a un modelo contener otros modelos de forma transparente a la vista, mientras por detrás de escena cada modelo gestiona sus propios datos.

from openerp import models
class TodoTask(models.Model):
    _name = 'todo.task'
    _inherit = 'mail.thread'


esto amplia el modelo todo.task copiando las caracteristícas del modelo mail.thread el cual imple,menta mensajería de Odoo y la función de seguidores, y es reusable, por lo tanto es fácil agregar esas características a cualquier modelo. Los registros de datos del modelo original (heredado) y el nuevo modelo (heredero) son conservados sin relación entre ellos. Solo son compartidas las definiciones.

**Modelos Abstractos: son como los modelos regulares excepto que no es creada ninguna representación de ellos en la base de datos. Actúan como plantillas, describen campos y la lógica para ser reusadas en modelos regulares.

**Podemos usar mail.thread para agregar caracteristicas de redes sociales a nuestros módulos.

**Herencia Delegada:**  impide la duplicación de estructuras de datos, por lo que es usualmente usada cuando se hereda de modelos regulares. Es el método de extensión de modelos usado con menos frecuencia, pero puede proporcionar soluciones muy convenientes.
La ventaja de esto, comparada a la herencia por prototipo, es que no hay necesidad de repetir la estructura de datos en muchas tablas, como las direcciones. Cualquier modelo que necesite incluir un dirección puede delegar esto a un modelo Partner vinculado.
con la herencia delegada, los campos con heredados, pero los métodos no.

### Usar la herencia para agregar características redes sociales

Las características de mensajería de red social son proporcionadas por el modelo mail.thread del modelo mail. Para agregarlo a un módulo personalizado necesitamos:

1. Que el módulo dependa de mail.
1. Que la clase herede de mail.thread.
1. Tener agregados a la vista de formulario los widgets Followers (seguidores) y Threads (hilos).
1. Opcionalmente, configurar las reglas de registro para seguidores.





