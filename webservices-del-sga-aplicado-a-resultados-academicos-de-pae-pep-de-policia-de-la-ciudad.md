---
description: >-
  07/02/2022 - Documento de Especificación de Web Services para la Integración
  con el Sistema de Gestión Académica del ISSP para Notas y Asistencia del PAE y
  PEP
---

# Webservices del SGA aplicado a resultados académicos de PAE, PEP de Policia de la Ciudad

### Especificación de Servicios Externos Disponibles

#### Obtener resultados del PEP entre fechas <a href="#_toc1452381201" id="_toc1452381201"></a>

Devuelve un listado de los alumnos y sus resultados\
\
**Invocación**\
Se debe invocar mediante GET la sig. URL:\
[**https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerResultados**](https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerResultados)****\
****\
******Parámetros**\
`fechaDesde = en formato YYYY-mm-DD (ejemplo: 2021-08-24)`\
`fechaHasta = en formato YYYY-mm-DD (ejemplo: 2021-08-27)`\
``\
``**Respuesta**\
Este es un ejemplo de respuesta al método ObtenerResultados:

```
<string xmlns="http://tempuri.org/">{"FechaSolicitud":"2021-11-08T10:11:24.7550867-03:00","Resultados":[{"Apellido":"ACEVEDO","Nombre":"FABRIZIO EDGARDO","Email":"facevedo@buenosaires.gob.ar","Grado":"Oficial Primero","DNI":35033155,"LP":"3472","Resultado":"APROBADO","AS_ID":11794,"Fecha":"2021-08-24T00:00:00"},
{"Apellido":"ACOSTA","Nombre":"GUILLERMO FERNANDO","Email":"guillermofernandoacosta@gmail.com","Grado":"Oficial Primero","DNI":31967186,"LP":"9508","Resultado":"APROBADO","AS_ID":12322,"Fecha":"2021-08-25T00:00:00"},
{"Apellido":"ACOSTA","Nombre":"VALERIA SOLEDAD","Email":"vale85sol@hotmail.com","Grado":"Principal","DNI":31828825,"LP":"75190","Resultado":"DESAPROBADO","AS_ID":11053,"Fecha":"2021-08-24T00:00:00"}]
</string>
```

#### Obtener asistencia al PEP entre fechas

Devuelve un listado de alumnos y su asistencia a los turnos entre las fechas indicadas

&#x20;**Invocación**\
****Se debe invocar mediante POST la sig. URL:\
[**https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerAsistencia**](https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerAsistencia)****\
****\
**Parámetros**\
****fechaDesde = en formato YYYY-mm-DD (ejemplo: 2021-08-24)\
fechaHasta = en formato YYYY-mm-DD (ejemplo: 2021-08-27)\
Pasando el id de comisión obtenido con el método anterior recibirá la siguiente respuesta.\
\
**Respuesta**\
****Este es un ejemplo de respuesta al método obtenerAsistencia:

```
<string xmlns="http://tempuri.org/">[{"DNI":26062063,"LP":"595","AS_ID":"9946","EstadoAsistencia":"P","Observacion":"","Fecha":"2021-08-05T00:00:00"},
{"DNI":25149601,"LP":"699","AS_ID":"13924","EstadoAsistencia":"P","Observacion":"","Fecha":"2021-08-04T00:00:00"},
{"DNI":25766947,"LP":"721","AS_ID":"14559","EstadoAsistencia":"P","Observacion":"","Fecha":"2021-08-03T00:00:00"},
{"DNI":28585033,"LP":"776","AS_ID":"11040","EstadoAsistencia":"A","Observacion":"","Fecha":"2021-08-05T00:00:00"},
{"DNI":28369495,"LP":"811","AS_ID":"14752","EstadoAsistencia":"P","Observacion":"","Fecha":"2021-08-03T00:00:00"}]
</string>
```

#### Obtener resultados de Entrenamiento

Devuelve un listado con los resultados (que es la asistencia) del entrenamiento anual de tiro\
\
**Invocación**\
Se debe invocar mediante POST la sig. URL:\
[https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerResultadosEntrenamiento](https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerResultadosEntrenamiento)\
\
**Parámetros**\
fechaDesde = en formato YYYY-mm-DD (ejemplo: 2021-08-24)\
fechaHasta = en formato YYYY-mm-DD (ejemplo: 2021-08-27)\
\
**Respuesta**

```
<string xmlns="http://tempuri.org/"> 
{"FechaSolicitud":"2022-02-08T12:30:07.5524038-03:00","Resultados":[{"Apellido":"HERRERA","Nombre":"ANDRES GERMAN","DNI":27691430,"LP":"767","AS_ID":53484,"Fecha":"07/02/2022","Aprobo":"True"},
{"Apellido":"VAZQUEZ","Nombre":"FERNANDO MARTIN","DNI":26377227,"LP":"789","AS_ID":54801,"Fecha":"07/02/2022","Aprobo":"True"},
{"Apellido":"ZELAYA","Nombre":"WALTER OMAR","DNI":25231833,"LP":"835","AS_ID":60404,"Fecha":"07/02/2022","Aprobo":"True"},
{"Apellido":"NARVAJA","Nombre":"EDGARDO","DNI":12924613,"LP":"847","AS_ID":53877,"Fecha":"07/02/2022","Aprobo":"True"},{"Apellido":"LAVOLPE","Nombre":"EZEQUIEL MAXIMILIANO","DNI":31684838,"LP":"864","AS_ID":57180,"Fecha":"07/02/2022","Aprobo":"False"},
{"Apellido":"DELGADO","Nombre":"ALEJANDRO DAMIAN","DNI":30762416,"LP":"901","AS_ID":54161,"Fecha":"07/02/2022","Aprobo":"False"},
{"Apellido":"MARTINEZ","Nombre":"MARIO ANTONIO","DNI":20549752,"LP":"926","AS_ID":53155,"Fecha":"07/02/2022","Aprobo":"False"},
{"Apellido":"LUCIANO BERNARDO GABRIEL","Nombre":"FARINA","DNI":27024784,"LP":"933","AS_ID":54637,"Fecha":"07/02/2022","Aprobo":"False"},
{"Apellido":"CARDOZO","Nombre":"BEATRIZ GRISELDA","DNI":14985773,"LP":"1016","AS_ID":62021,"Fecha":"07/02/2022","Aprobo":"False"},
{"Apellido":"DELGADO MARTINEZ","Nombre":"ROSANA","DNI":26995706,"LP":"1116","AS_ID":53411,"Fecha":"07/02/2022","Aprobo":"False"}}]
</string>
```

#### Asignación de turno

Reagendar un turno presencial para el ISSP\
\
**Invocación**\
[https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=AsignacionTurno](https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=AsignacionTurno)\
\
**Parámetro**\
Recibe un json con el siguiente formato:\
`{'Fecha':'20210810','HoraTurno':'10:00','AS_ID':'0','LP':'2179','Convocatoria_Id':'1','Email':'pablo.betanzo@policiadelaciudad.gob.ar','ArmaNro':'PX6753L','Jerarquia':'Inspector'}`\
``\
``**Respuesta**\
****Si el registro se graba correctamente devuelve el siguiente mensaje: \
`“Se ha insertado el turno de asignación directa correctamente”`

#### Asignación de turno Entrenamiento

Reagendar un turno presencial para el ISSP para el PAE\
``\
``**Invocación**\
[https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=AsignacionTurnoEntrenamiento](https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=AsignacionTurnoEntrenamiento)\
\
**Parámetro**\
Recibe un json con el siguiente formato:\
`{'Fecha':'20220210','HoraTurno':'12:00','AS_ID':'54801','LP':'767','Convocatoria_Id':'4272','DNI':'26377227'}`\
\
**Respuesta**\
Si el registro se graba correctamente devuelve el siguiente mensaje:\
`“Se ha insertado el turno de asignación directa correctamente”`
