---
description: >-
  08/12/2021 - Documento de Especificación de Web Services para la Integración
  con el Sistema de Gestión Académica del ISSP para Notas y Asistencia del PEP
---

# Webservices del SGA aplicado a resultados académicos de Plan de Evaluación Permanente (PEP) Policía

### Especificación de Servicios Externos Disponibles

#### Obtener resultados del PEP entre fechas

Devuelve un listado de los alumnos y sus resultados

**Invocación**\
Se debe invocar mediante GET la sig. URL:\
[**https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerResultados**](https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerResultados)\
**Parámetros**\
****`fechaDesde = en formato YYYY-mm-DD (ejemplo: 2021-08-24)`\
`fechaHasta = en formato YYYY-mm-DD (ejemplo: 2021-08-27)`\
``**Respuesta**\
****Este es un ejemplo de respuesta al método ObtenerResultados:

```
<string xmlns="http://tempuri.org/">{"FechaSolicitud":"2021-11-08T10:11:24.7550867-03:00","Resultados":[{"Apellido":"ACEVEDO","Nombre":"FABRIZIO EDGARDO","Email":"facevedo@buenosaires.gob.ar","Grado":"Oficial Primero","DNI":35033155,"LP":"3472","Resultado":"APROBADO","AS_ID":11794,"Fecha":"2021-08-24T00:00:00"},
{"Apellido":"ACOSTA","Nombre":"GUILLERMO FERNANDO","Email":"guillermofernandoacosta@gmail.com","Grado":"Oficial Primero","DNI":31967186,"LP":"9508","Resultado":"APROBADO","AS_ID":12322,"Fecha":"2021-08-25T00:00:00"},
{"Apellido":"ACOSTA","Nombre":"VALERIA SOLEDAD","Email":"vale85sol@hotmail.com","Grado":"Principal","DNI":31828825,"LP":"75190","Resultado":"DESAPROBADO","AS_ID":11053,"Fecha":"2021-08-24T00:00:00"}]
</string>
```

#### Obtener asistencia al PEP entre fechas

Devuelve un listado de alumnos y su asistencia a los turnos entre las fechas indicadas

**Invocación**\
Se debe invocar mediante POST la sig. URL:\
[**https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerAsistencia**](https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerAsistencia)****\
**Parámetros**\
fechaDesde = en formato YYYY-mm-DD (ejemplo: 2021-08-24)\
fechaHasta = en formato YYYY-mm-DD (ejemplo: 2021-08-27)\
Pasando el id de comisión obtenido con el método anterior recibirá la siguiente respuesta.\
**Respuesta**\
Este es un ejemplo de respuesta al método obtenerAsistencia:

```
<string xmlns="http://tempuri.org/">[{"DNI":26062063,"LP":"595","AS_ID":"9946","EstadoAsistencia":"P","Observacion":"","Fecha":"2021-08-05T00:00:00"},
{"DNI":25149601,"LP":"699","AS_ID":"13924","EstadoAsistencia":"P","Observacion":"","Fecha":"2021-08-04T00:00:00"},
{"DNI":25766947,"LP":"721","AS_ID":"14559","EstadoAsistencia":"P","Observacion":"","Fecha":"2021-08-03T00:00:00"},
{"DNI":28585033,"LP":"776","AS_ID":"11040","EstadoAsistencia":"A","Observacion":"","Fecha":"2021-08-05T00:00:00"},
{"DNI":28369495,"LP":"811","AS_ID":"14752","EstadoAsistencia":"P","Observacion":"","Fecha":"2021-08-03T00:00:00"}]
</string>
```

#### Obtener resultados de Entrenamiento anual de tiro

**Invocación**\
Se debe invocar mediante POST la sig. URL:[\
https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerResultadosEntrenamientoTiro](https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerResultadosEntrenamientoTiro)\
**Parámetros**\
`fechaDesde = en formato YYYY-mm-DD (ejemplo: 2021-08-24)`\
`fechaHasta = en formato YYYY-mm-DD (ejemplo: 2021-08-27)`\
**Respuesta**

```
<string xmlns="http://tempuri.org/">{"FechaSolicitud":"2021-11-08T10:30:21.8346485-03:00","Resultados":[{"Apellido":"LINARES","Nombre":"LORENA VANESA","DNI":29218173,"LP":"2107","AS_ID":20928,"Fecha":"2021-08-25T00:00:00"},
{"Apellido":"RODRIGUEZ","Nombre":"CINTIA VANESA","DNI":34156213,"LP":"2358","AS_ID":27939,"Fecha":"2021-08-10T00:00:00"},
{"Apellido":"GARNICA","Nombre":"MARLENE","DNI":32341543,"LP":"2282","AS_ID":25427,"Fecha":"2021-08-10T00:00:00"},
{"Apellido":"MANSILLA","Nombre":"MARIANO DAVID","DNI":29531659,"LP":"2129","AS_ID":20155,"Fecha":"2021-08-10T00:00:00"}"}]
</string>
```

#### Asignación de turno

Reagendar un turno presencial para el ISSP\
**Invocación**\
[https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=AsignacionTurno](https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=AsignacionTurno)\
**Parámetro**\
Recibe un json con el siguiente formato:\
`{'Fecha':'20210810','HoraTurno':'10:00','AS_ID':'0','LP':'2179','Convocatoria_Id':'1','Email':'pablo.betanzo@policiadelaciudad.gob.ar','ArmaNro':'PX6753L','Jerarquia':'Inspector'}`\
**Respuesta**\
Si el registro se graba correctamente devuelve el siguiente mensaje:\
`“Se ha insertado el turno de asignación directa correctamente”`
