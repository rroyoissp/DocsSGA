# Guía rápida de métodos de Entrenamiento Anual, PEP y Ascenso

### Procesamiento de turnos

| **Etapa**           | **Interfaz SGA**                       | **Procedimiento Almacenado**            |
| ------------------- | -------------------------------------- | --------------------------------------- |
| Entrenamiento Anual | PEA/ProcesarTurnosEntrenamientoWS.aspx | PAE\_ImportarTurnosEntrenamientoAnualWS |
| PEP                 | PEA/PEP\_ProcesarInscriptos.aspx       | PAE\_ImportarTurnosDesdeWS              |
| Ascenso             | PEA/PEP\_ProcesarInscriptos            | PAE\_ImportarAscensoWS                  |

&#x20;

### Asignación de turnos desde los servicios webs

| **Etapa**           | **Servicio web y método**                         | **Procedimiento Almacenado** |
| ------------------- | ------------------------------------------------- | ---------------------------- |
| Entrenamiento Anual | ServiciosPEP.asmx?op=AsignacionTurnoEntrenamiento | ENTRENAMIENTO\_AsignarTurno  |
| PEP                 | ServiciosPEP.asmx?op=AsignacionTurno              | PEP\_ProcesarTurnos          |
| Ascenso             | ServiciosPCBA.asmx?op=ReasignarTurnoExamenAscenso | ASCENSO\_AsignarTurno        |

&#x20;

### Obtener resultados desde servicios webs

| **Etapa**           | **Servicio web y método**                           | **Procedimiento Almacenado**              |
| ------------------- | --------------------------------------------------- | ----------------------------------------- |
| Entrenamiento Anual | ServiciosPEP.asmx?op=ObtenerResultadosEntrenamiento | PEP\_WS\_ObtenerResultados\_Entrenamiento |
| PEP                 | ServiciosPEP.asmx?op=ObtenerResultados              | Rpt\_Pep\_Acta                            |
| Ascenso             | ServiciosPCBA.asmx?op=getResultadosAscenso          | RPT\_ACA\_ResultadoAscenso                |

&#x20;

### Obtener asistencia desde servicios webs

| **Etapa** | **Servicio web y método**              | **Procedimiento Almacenado** |
| --------- | -------------------------------------- | ---------------------------- |
| PEP       | ServiciosPEP.asmx?op=ObtenerAsistencia | PEP\_WS\_ObtenerAsistencia   |

&#x20;

### Inscribir en Moodle

| **Etapa**           | **Servicio y método**           |  ****                               |
| ------------------- | ------------------------------- | ----------------------------------- |
| Entrenamiento Anual |                                 | Se inscriben al procesar los turnos |
| PEP                 | ISSP\_PEP\ISSP\_HabilitarMoodle | Proceso que corre todos los días    |
| Ascenso             |                                 | Se inscriben al procesar los turnos |
