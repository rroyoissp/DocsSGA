---
description: >-
  Objetivo: Enumerar y realizar breve descripción sobre los servicios
  automáticos que están corriendo en el ISSP.
---

# Servicios automáticos

### Descripción general de la solución para procesos automáticos

Servicios de Windows desarrollado con C# y Net Framework 4.5\
Instalados y corriendo en el servidor 10.26.250.233

#### WormHole\_Service (servidor 10.26.250.233)

Proyecto Net: ISSP\_WormHole (temporal hasta que esté el nuevo servicio en Xojo)\
Conecta con Moodle a través de los webservices desarrollados por la plataforma para traer las notas de los alumnos agendados para rendir en el día anterior, algún curso de seguridad privada. Graba la nota, genera el QR y el certificado y lo envía por mail.\
Frecuencia de ejecución: se ejecuta 3 veces al día, 3.10, 9.10 y 15.10 horas.

#### SegPrivMoodle (servidor 10.26.250.233)

Proyecto Net: ISSP\_SeguridadPrivadaMoodle\
Busca las inscripciones pendientes de seguridad privada para inscribir los alumnos en los cursos, tanto en nuestra base de datos como en WormHole.\
Utiliza las API’s de WH para dicha inscripción. Frecuencia de ejecución: \*\*\* .

#### Moodle\_ProgressService  (servidor 10.26.250.233)

Proyecto Net: ISSP\_ControlProgresoMoodle\
Recorre todas las personas que están cursando los cursos de seguridad privada en Moodle y actualiza su progreso en nuestra base de datos. Utiliza los webservice de Moodle.\
Frecuencia de ejecución: cada 1 hora.
