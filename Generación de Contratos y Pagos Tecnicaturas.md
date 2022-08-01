---
description: 10/02/2021 - Gabriel Benitez
---

# Generación de Contratos y Pagos Tecnicaturas

### **Historia de revisiones del documento**

10/02/2022 - Gabriel Benitez: Creación del documento

### Problemática

Describir el proceso y las funciones y métodos involucrados desde la inscripción de un alumno hasta la imputación del pago en el Sistema de Gestión Académica (SGA).

### Contenidos

A continuación, se enumeran los pasos y las interfaces y métodos involucrados en cada uno de ellos

#### Generación del contrato

La inscripción a una de las tecnicaturas implica la creación de un contrato que relacione al alumno con el plan de estudio. Esto se realiza desde la interfaz Tesorería / Contrato y cuotas.

Se graba y se genera el contrato usando el procedimiento almacenado “GeneraContrato” con sol siguientes parámetros:

| Campo              | Valor a grabar - Tipo de dato             | Observación                                                                                                                                                                                                                                                                                                                                                                                          |
| ------------------ | ----------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PersonaId          | Id del alumno - int                       | Se obtiene de la interfaz, alumno seleccionado                                                                                                                                                                                                                                                                                                                                                       |
| FechaInicio        | Fecha inicio del contrato - datetime      | Se obtiene de la interfaz                                                                                                                                                                                                                                                                                                                                                                            |
| FechaFin           | Fecha fin del contrato - datetime         | Se calcula, último dia del año en curso                                                                                                                                                                                                                                                                                                                                                              |
| TitularRecibo      | Nombre que llevaría el recibo - varchar   | Se obtiene de la interfaz (en desuso)                                                                                                                                                                                                                                                                                                                                                                |
| Descuento          | Descuento si se aplicará - decimal        | Se graba 0 por default                                                                                                                                                                                                                                                                                                                                                                               |
| CarreraId          | Id de carrera - int                       | <p>Se obtiene de la interfaz, carrera seleccionada.</p><p>Hay dos opciones para mostrar las carreras:</p><p>1) Que el alumno tenga un registro en tabla Postulación, que se completaba desde la página web del ISSP (en desuso?)</p><p>2) Que el alumno tenga un contrato previo en alguna carrera</p><p>NOTA: ¿Qué pasa con alumnos nuevos si punto 1 está en desuso? ¿Cuál es circuito actual?</p> |
| ImporteFijoPorHora | decimal                                   | Solo se graba si el plan no tiene planes de pago (en desuso)                                                                                                                                                                                                                                                                                                                                         |
| PlanEstudioId      | Id del plan de estudio seleccionado - int | Se obtiene de la interfaz, plan de estudio seleccionado, que se muestra al elegir la carrera, y solo con planes de estudio vigentes, si la carrera tiene planes                                                                                                                                                                                                                                      |
| PlanPagoId         | Id del plan de pagos - int                | Se obtiene de la interfaz, plan de pago seleccionado. Si la carrera tiene planes de pago asociados.                                                                                                                                                                                                                                                                                                  |
| Estado             | Estado del plan a dar de alta - varchar   | El estado del plan se obtiene de la interfaz, actualmente está fijado en “A” (Activo) y no se puede cambiar.                                                                                                                                                                                                                                                                                         |
| ConceptoIngresoId  | Concepto de ingreso de tesorería - int    | Se obtiene de la interfaz, concepto seleccionado de la lista.                                                                                                                                                                                                                                                                                                                                        |
| Nota               | Nota que acompaña al contrato - varchar   | Se obtiene de la intefaz, campo al lado de beca, generalmente se usa para acompañar una beca                                                                                                                                                                                                                                                                                                         |
| Beca               | Indica si es o no una beca - bit          | Se obtiene de la interfaz, 1 o 0, dependiendo si se otorga beca o no.                                                                                                                                                                                                                                                                                                                                |
| Usuario            | Usuario logueado al SGA - varchar         | Se obtiene del SGA, el nombre del usuario logueado al sistema.                                                                                                                                                                                                                                                                                                                                       |

El procedimiento “GenerarContrato” realiza las siguientes acciones:

1. Valida que el alumno no tiene un contrato vigente para ese plan de estudio, dentro del rango fecha de inicio y fin del contrato.\

2. Inserta un registro en la tabla “ContratoAlumno” con los valores pasados como parámetros.\

3. De acuerdo al plan de pago pasado como parámetro y la cantidad de cuotas del mismo se crean los registros en las tablas

&#x20;         a. AlumnoDevengado:

| Campo       | Valor a grabar - Tipo de dato           | Observación                                                                                                                                                                                                             |
| ----------- | --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Vencimiento | Fecha de vencimiento – datetime         | Es la fecha de vencimiento de la cuota, este dato es informado por Tesorería del ISSP y está “harcodeado” en el procedimiento “GenerarContrato” y está preparado para un máximo de 3 cuotas (pendiente de modificación) |
| Nota        | Nota que acompaña al contrato - varchar | Se utiliza en general con becas                                                                                                                                                                                         |
| Fecha       | Fecha de grabación del registro         | Se graba fecha y hora actual                                                                                                                                                                                            |
| Estado      | Estado de la cuota – vachar             | Se graba "P” de Pendiente.                                                                                                                                                                                              |
| PersonaId   | Id del alumno – int                     | Se recibe como parámetro                                                                                                                                                                                                |

&#x20;         b. AlumnoDevengadoDetalle:

| Campo              | Valor a grabar - Tipo de dato           | Observación                                                                                                                                                                  |
| ------------------ | --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AlumnoDevenegadoId | Id de tabla AlumnoDevenegado - int      | Es el id generado en el paso anterior (3.a) al insertar el registro en la tabla AlumnoDevenegado                                                                             |
| ContratoAlumnoId   | Id del contrato – int                   | Es el id generado en el paso 2 al insertar el registro en la tabla ContratoAlumno                                                                                            |
| Importe            | Importe de la cuota – decimal           | Se obtiene del plan de pago seleccionado y recibido como parámetro, es igual al monto total del plan dividido la cantidad de cuotas (Plan.Monto), si es beca graba 0 (cero). |
| ConceptoIngresoId  | Concepto de ingreso de tesorería - int  | Recibido como parámetro.                                                                                                                                                     |
| Descuento          | Descuento aplicado a la cuota – decimal | Se graba siempre 0 (cero) (en desuso)                                                                                                                                        |
| Beca               | Valor de la beca – decimal              | Si es beca se graba el importe de la cuota, sino 0 (cero)                                                                                                                    |
| CuotaNumero        | Numero de la cuota – int                | Se graba le número de la cuota (1, 2 o 3)                                                                                                                                    |

