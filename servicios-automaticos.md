Servicios automáticos
Objetivo: Enumerar y realizar breve descripción sobre los servicios automáticos que están corriendo en el ISSP.
Descripción general de la solución para procesos automáticos
 Proyecto Net: ISSP_WormHole (temporal hasta que esté el nuevo servicio en Xojo) 
 Conecta con Moodle a través de los webservices desarrollados por la plataforma para traer las notas de los alumnos agendados para rendir en el día anterior, algún curso de seguridad privada. Graba la nota, genera el QR y el certificado y lo envía por mail. 
 Frecuencia de ejecución: se ejecuta 3 veces al día, 3.10, 9.10 y 15.10 horas.
Nombre del Servicio: SegPrivMoodle (servidor 10.26.250.233) 
 Proyecto Net: ISSP_SeguridadPrivadaMoodle 
 Busca las inscripciones pendientes de seguridad privada para inscribir los alumnos en los cursos, tanto en nuestra base de datos como en WormHole. Utiliza las API’s de WH para dicha inscripción.
 Frecuencia de ejecución: *** .
Nombre del Servicio: Moodle_ProgressService (servidor 10.26.250.233)
 Proyecto Net: ISSP_ControlProgresoMoodle 
Recorre todas las personas que están cursando los cursos de seguridad privada en Moodle y actualiza su progreso en nuestra base de datos. Utiliza los webservice de Moodle. 
Frecuencia de ejecución: cada 1 hora.
Nombre del Servicio: SegPriv_Service
Proyecto Net: ISSP_SeguridadPrivada
Busca las inscripciones pendientes de seguridad privada para inscribir los alumnos en los cursos, tanto en nuestra base de datos como en WormHole. Utiliza las API’s de WH para dicha inscripción.
Frecuencia de ejecución: cada 1 minuto .
Nombre del Servicio: RENAPER_UpdateImages
Proyecto Net: ISSP_Renaper
Recorre todas las personas de nuestra base de datos y consulta servicio web de Policía de la Ciudad que conecta con otro del RENAPER para traer la foto, actualizar fecha de nacimiento, cuil y sexo desde el Registro Nacional de las Personas.
Frecuencia de ejecución: cada 3 meses. 
Nombre del Servicio: WormHole_ProgressService 
Proyecto Net: ISSP_ControlProgresoWH Recorre todas las personas que están cursando los cursos de seguridad privada en WormHole y actualiza su progreso en nuestra base de datos. Utiliza las API’s de WH. Frecuencia de ejecución: cada 1 hora.
Nombre del Servicio: ISSP_ControlBUIs_Service (NO IMPLEMENTADO EN PRODUCCION)
 Proyecto Net: ISSP_ControlBUIs Utiliza los servicios web de Hacienda para buscar BUIs pagas en el día de la fecha para los conceptos de cursos de seguridad privada y los agrega a la cuenta corriente de cada empresa en nuestra base de datos. Frecuencia de ejecución: diario a las 22.00PM.
Nombre del Servicio: ISSP_CAE 
Proyecto Net: ISSP_CAE 
Utiliza los servicios web de Policía de la Ciudad para buscar convocatorias creadas, inscriptos a convocatorias y controlar actas cerradas para cursos de planes de estudio que pertenecen a escuela de especialidades.
 Frecuencia de ejecución: diario a las 22.10PM, ejecuta el Control de Actas, 23.10 ejecuta la obtención de nuevas convocatorias, 23.30 ejecuta la importación de alumnos inscriptos.