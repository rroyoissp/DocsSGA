# Entrenamiento Anual Descripción

### Historia de Revisiones del Documento

08/02/2022 - Gabriel Benitez - Creación del documento

### Problemática

Describir el circuito para PAE, indicando sistemas e interfaces intervinientes.

### Contenidos

El Plan de Entrenamiento Anual, de acá en más PAE, consta de 3 etapas:

1\) **Obtener y procesar turnos.** En esta etapa se utiliza el SGA, accediendo a la interfaz “P A E / Procesar Turnos de Entrenamiento”. El proceso está descripto en el documento “FUNC-Procesar Inscriptos PAE.docx”

2\) **Recepción del personal.** También el SGA se encuentra la interfaz para recepción, “P A E / Recepción Entrenamiento”. En esta interfaz se lee el DNI con las lectoras o se ingresa el número manualmente y el sistema valida el turno, de existir dicho turno para el día marca como aprobado el contrato para el plan de estudio PAE(tener en cuenta que solo presentarse implica aprobación del PAE), del semestre que corresponda. Antes del 30/06 marca aprobado el contrato del primer semestre, caso contrario el del segundo semestre.

**NOTA**: Utiliza el procedimiento almacenado “_PEP\_ValidarEntrenamiento_”

3\) **Devolver resultados.** Para la devolución de resultados se deja disponible un método de servicio web llamado “ObtenerResultadosEntrenamiento” ([https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerResultadosEntrenamiento](https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=ObtenerResultadosEntrenamiento))

**NOTA**: Descripto en el documento FUNC-Especificación de Servicios Externos Disponibles PCBA PAE\_PEP\_v2.docx, utiliza el procedimiento almacenado “R_PT\_PEP\_WS\_ObtenerResultados\_Entrenamiento_”.

4\) **Reasignar turnos para PAE.** Para permitir la reasignación de turnos existe otro método en el servicio web denominado “AsignacionTurnoEntrenamiento” ([https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=AsignacionTurnoEntrenamiento](https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=AsignacionTurnoEntrenamiento))

**NOTA**: Descripto en el documento FUNC-Especificación de Servicios Externos Disponibles PCBA PAE\_PEP\_v2.docx, utiliza el procedimiento almacenado “_ENTRENAMIENTO\_AsignarTurno_”.

### Especificaciones para llamadas a procedimientos

#### PEP\_ValidarEntrenamiento

PersonaId: id de persona , tipo de dato entero.

FechaHora: Fecha hora actual, tipo de dato datetime

#### RPT\_PEP\_WS\_ObtenerResultados\_Entrenamiento

FechaDesde: fecha de inicio para consultar datos, tipo de dato datetime.

FechaHasta: fecha de fin para consultar datos, tipo de dato datetime.

#### ENTRENAMIENTO\_AsignarTurno

Fecha: fecha para el nuevo turno, tipo de dato datetime.

DNI: número de documento de la persona a la que se va a reasignar el turno, tipo de dato entero.

AS\_ID: id de asignación de CAE, tipo de dato entero.

Nota: observación que se grabará en el turno, tipo de dato varchar.

HoraTurno: hora del nuevo turno, con formato HH:MM, tipo de dato varchar.
