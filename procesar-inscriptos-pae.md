# Procesar Inscriptos PAE

## Historia de Revisiones del Documento

04/02/2022 - Gabriel Benitez - Creación del documento

### Problemática

Describir el proceso y las funciones y métodos involucrados para la importación de inscriptos en CAE para el entrenamiento anual y la generación de turnos en el ISSP e inscripción a cursos.

### Contenidos

Para obtener la lista de inscriptos para el PAE (Plan de Entrenamiento Anual) del sistema CAE se utilizan los métodos del servicio web [_**http://10.74.50.114/wsIntegracionissp/server.php?wsdl**_](http://10.74.50.114/wsIntegracionissp/server.php?wsdl) _****_ , llamados desde la interfaz del SGA _(_[_**http://academico.insusep.edu.ar/instituto/**_](http://academico.insusep.edu.ar/instituto/)_**)**_ a la que se accede desde el menú PAE / Procesar Turnos de Entrenamiento.

1\)      Se selecciona el plan de estudio y el rango de fechas para obtener los inscriptos en esas fechas.

_**2)**_      Se utiliza el método de ws para obtener los turnos _**consultaAsignacion(fechaDesde, fechaHasta, "1", "usuario", "10.209.33.179")**_ , siendo el formato de fecha requerido dd/MM/aaaa

_**3)**_      Se recorre el listado obtenido ejecutando para cada ítem el procedimiento almacenado _**PAE\_ImportarTurnosEntrenamientoAnualWS**_ con la siguiente lista de parámetros

| **Parámetro**                 | **Tipo de dato** | **Valor**                                          |
| ----------------------------- | ---------------- | -------------------------------------------------- |
| @Fecha                        | DateTime         | item.Convocatoria\_Fecha “Fecha del turno“         |
| @HoraTurno                    | Varchar          | item.HoraTurno “Hora del turno (formato: HH:MM)”   |
| @AS\_ID                       | Int              | item.Asignacion\_Id                                |
| @Legajo                       | Varchar          | item.Personal\_Legajo                              |
| @DNI                          | Varchar          | Item.Personal\_DNI                                 |
| @PlanEstudioId                | Int              | cboPlanEstudio “Valor seleccionado en la pantalla” |
| @LogImportacionTurnoProcesoId | Int              | “Id del proceso automático de la tabla de logs”    |
| @Etapa\_Cone\_id              | Int              | “vacío, en desuso”                                 |
| @Convocatoria\_id             | Int              | Item.Convocatoria\_Id                              |
| @NroArma                      | Varchar          | Item.Personal\_Arma                                |
| @Jerarquia                    | Varchar          | Item.Personal\_Grado                               |
| @EstadoPolicial               | Varchar          | Item.Estado\_Policial                              |

&#x20;

4\)      Se vuelve a recorrer el listado obtenido para, por cada ítem, llamar al método de inscripción en el curso de Moodle correspondiente, para eso se utilizan los métodos del servicio web de Moodle [_**https://webcampus.insusep.edu.ar/webservice/rest/server.php?wstoken=e9360ce79d93f3cee654028dbb012d62**_](https://webcampus.insusep.edu.ar/webservice/rest/server.php?wstoken=e9360ce79d93f3cee654028dbb012d62) _****_ (ISSP) o [_**https://iusecampus.insusep.edu.ar/webservice/rest/server.php?wstoken=14966b3a88f9327c7e7243411b09da1f**_](https://iusecampus.insusep.edu.ar/webservice/rest/server.php?wstoken=14966b3a88f9327c7e7243411b09da1f) _****_ (IUSE):

| **Llamadas a métodos de ws usados**                                                                                                                                        |  ****                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| core\_user\_get\_users\_by\_field\&moodlewsrestformat=json\&field=username\&values\[0]=" + username;                                                                       | Para obtener el usuario            |
| core\_user\_create\_users\&moodlewsrestformat=json\&users\[0]\[username]=" + nombreUsuario + "\&users\[0]\[firstname]=" + nombre + "\&users\[0]\[lastname]=" + apellido    | Para crear el usuario si no existe |
| core\_user\_update\_users\&moodlewsrestformat=json\&users\[0]\[id]=" + userid + "\&users\[0]\[password]=" + clave                                                          | Para actualizer el password        |
| enrol\_manual\_enrol\_users\&moodlewsrestformat=json\&enrolments\[0]\[roleid]=" + role + "\&enrolments\[0]\[userid]=" + userid + "\&enrolments\[0]\[courseid]=" + courseid | Para inscribir a un curso          |
