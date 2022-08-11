---
description: >-
  Objetivo: Enumerar y realizar breve descripción sobre los servicios
  automáticos que están corriendo en el ISSP.
---

# Servicios automáticos

### Descripción general de la solución para procesos automáticos

Servicios de Windows desarrollado con C# y Net Framework 4.5\
Instalados y corriendo en el servidor 10.26.250.233

**ISSP\_MoodleSegPriv.exe**&#x20;

#### Nombre del Servicio: ISSP\_MoodleSegPriv (servidor 10.26.250.233)&#x20;

Proyecto Net: ISSP\_MoodleSegPriv (temporal hasta que esté el nuevo servicio en Xojo)\
&#x20;Conecta con Moodle a través de los webservices desarrollados por la plataforma para traer las notas de los alumnos agendados para rendir en el día anterior, algún curso de seguridad privada. Graba la nota, genera el QR y el certificado y lo envía por mail.\
&#x20;Frecuencia de ejecución: se ejecuta 3 veces al día, 3.10, 9.10 y 15.10 horas.

#### ~~Nombre del Servicio: WormHole\_Service (servidor 10.26.250.233)~~&#x20;

&#x20;~~Proyecto Net: ISSP\_WormHole (temporal hasta que esté el nuevo servicio en Xojo)~~ \
&#x20;~~Conecta con Moodle a través de los webservices desarrollados por la plataforma para traer las notas de los alumnos agendados para rendir en el día anterior, algún curso de seguridad privada. Graba la nota, genera el QR y el certificado y lo envía por mail.~~ \
&#x20;~~Frecuencia de ejecución: se ejecuta 3 veces al día, 3.10, 9.10 y 15.10 horas.~~

#### Nombre del Servicio: SegPrivMoodle (servidor 10.26.250.233)&#x20;

&#x20;Proyecto Net: ISSP\_SeguridadPrivadaMoodle \
&#x20;Busca las inscripciones pendientes de seguridad privada para inscribir los alumnos en los cursos, tanto en nuestra base de datos como en WormHole. Utiliza las API’s de WH para dicha inscripción.\
~~~~ Frecuencia de ejecución: \*\*\* .

#### Nombre del Servicio: Moodle\_ProgressService (servidor 10.26.250.233)

&#x20;Proyecto Net: ISSP\_ControlProgresoMoodle \
Recorre todas las personas que están cursando los cursos de seguridad privada en Moodle y actualiza su progreso en nuestra base de datos. Utiliza los webservice de Moodle. \
Frecuencia de ejecución: cada 1 hora.

#### ~~Nombre del Servicio: SegPriv\_Service~~

~~Proyecto Net: ISSP\_SeguridadPrivada~~\
~~Busca las inscripciones pendientes de seguridad privada para inscribir los alumnos en los cursos, tanto en nuestra base de datos como en WormHole. Utiliza las API’s de WH para dicha inscripción.~~\
~~Frecuencia de ejecución: cada 1 minuto .~~

#### ~~Nombre del Servicio: RENAPER\_UpdateImages~~

~~Proyecto Net: ISSP\_Renaper~~\
~~Recorre todas las personas de nuestra base de datos y consulta servicio web de Policía de la Ciudad que conecta con otro del RENAPER para traer la foto, actualizar fecha de nacimiento, cuil y sexo desde el Registro Nacional de las Personas.~~\
~~Frecuencia de ejecución: cada 3 meses.~~&#x20;

#### ~~Nombre del Servicio: WormHole\_ProgressService~~&#x20;

~~Proyecto Net: ISSP\_ControlProgresoWH Recorre todas las personas que están cursando los cursos de seguridad privada en WormHole y actualiza su progreso en nuestra base de datos. Utiliza las API’s de WH. Frecuencia de ejecución: cada 1 hora.~~

#### ~~Nombre del Servicio: ISSP\_ControlBUIs\_Service (NO IMPLEMENTADO EN PRODUCCION)~~

&#x20;~~Proyecto Net: ISSP\_ControlBUIs Utiliza los servicios web de Hacienda para buscar BUIs pagas en el día de la fecha para los conceptos de cursos de seguridad privada y los agrega a la cuenta corriente de cada empresa en nuestra base de datos. Frecuencia de ejecución: diario a las 22.00PM.~~

#### ~~Nombre del Servicio: ISSP\_CAE~~&#x20;

~~Proyecto Net: ISSP\_CAE~~ \
~~Utiliza los servicios web de Policía de la Ciudad para buscar convocatorias creadas, inscriptos a convocatorias y controlar actas cerradas para cursos de planes de estudio que pertenecen a escuela de especialidades.~~\
&#x20;~~Frecuencia de ejecución: diario a las 22.10PM, ejecuta el Control de Actas, 23.10 ejecuta la obtención de nuevas convocatorias, 23.30 ejecuta la importación de alumnos inscriptos.~~
