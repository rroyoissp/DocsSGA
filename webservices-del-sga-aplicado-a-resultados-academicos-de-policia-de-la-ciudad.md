---
description: >-
  08/11/2021 - Documento de Especificación de Web Services para la Integración
  con el Sistema de Gestión Académica del ISSP para Notas de Ascenso
---

# Webservices del SGA aplicado a resultados académicos de Policía de la Ciudad

### Especificación de Servicios Externos Disponibles

#### Obtener las comisiones habilitadas para consulta de resultados

Devuelve un listado de comisiones habilitadas para consulta\
**Invocación**\
****Se debe invocar mediante GET la sig. URL:\
[**https://academico.insusep.edu.ar/WS-ServiciosISSP\_produccion/ServiciosPCBA.asmx?op=getComisionesAscensoHabilitadasConsulta**](https://academico.insusep.edu.ar/WS-ServiciosISSP\_produccion/ServiciosPCBA.asmx?op=getComisionesAscensoHabilitadasConsulta)****\
**Respuesta**\
****Este es un ejemplo de respuesta al método getComisionesAscensoHabilitadasConsulta:\
`<string xmlns="http://tempuri.org/">`\
`[{"id":2823,"Nombre":"1CAI2019-01TM"},{"id":2824,"Nombre":"1CAI2019-02TT"},{"id":2835,"Nombre":"1CAO2019-01TM"}]`\
`</string>`

#### Obtener las notas de ASCENSO para una comisión

Devuelve un listado de alumnos y sus notas\
**Invocación**\
Se debe invocar mediante POST la sig. URL:\
[**https://academico.insusep.edu.ar/WS-ServiciosISSP\_produccion/ServiciosPCBA.asmx?op=getResultadosAscenso**](https://academico.insusep.edu.ar/WS-ServiciosISSP\_produccion/ServiciosPCBA.asmx?op=getResultadosAscenso)\
Pasando el id de comisión obtenido con el método anterior recibirá la siguiente respuesta.\
**Respuesta**\
****Este es un ejemplo de respuesta al método getResultadosAscenso:

```
<string xmlns="http://tempuri.org/">[{"DNI":34848502,"Apellido":" DIAZ CASTELLANO","Nombre":"NICOLAS","Grado":"Inspector","Resultado":"DESAPROBADO","Fecha":"2021-07-06T11:30:00","Nota":5.00},
{"DNI":28384099,"Apellido":"ACOSTA","Nombre":" WALTER GUSTAVO","Grado":"Inspector","Resultado":"DESAPROBADO","Fecha":"2021-07-05T11:30:00","Nota":6.00},
{"DNI":17304558,"Apellido":"ACOSTA","Nombre":"MONICA PATRICIA","Grado":"Inspector","Resultado":"APROBADO","Fecha":"2021-07-05T12:30:00","Nota":8.00},
{"DNI":22664728,"Apellido":"AGUIRRE","Nombre":"ROBERTO RENE","Grado":"Inspector","Resultado":"APROBADO","Fecha":"2021-07-06T11:30:00","Nota":9.00},
{"DNI":24930084,"Apellido":"ALBERTI","Nombre":"JOSE RUBEN","Grado":"Inspector","Resultado":"APROBADO","Fecha":"2021-07-06T10:30:00","Nota":9.00}]
</string>
```

****
