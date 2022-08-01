# Entrenamiento Anual, PEP y Ascenso

### Historia de Revisiones del Documento

23/12/2021 - Gabriel Benitez - Creación del documento\
28/12/2021 - Gabriel Benitez - Modificación título y punto 1 y 3

### Problemática

A partir de los cambios en el proceso del plan de entrenamiento anual, se deben adaptar los sistemas de importación de turnos y el SGA para responder a estas modificaciones.

### Relevamiento

El entrenamiento anual ahora se divide en dos instancias a la que debe presentarse el personal para estar habilitado al PEP y Ascenso en el año posterior. Las instancias no llevan nota, pero deben registrarse los aciertos de tiro (en aquellos que corresponda), y la asistencia para los bomberos, eso implica la aprobación de las instancias.

### Contenidos

**Procesar turnos**

Se necesita un proceso de importación de turnos del entrenamiento anual que:

1\)      genere los turnos en SGA,

_**a.**_     Modificar la interfaz P A E / Procesar Turnos Entrenamiento\[GB1]&#x20;

_**b.**_ Utilizar el procedimiento almacenado _**PAE\_ImportarTurnosEntrenamientoAnualWS**_

_Importante: tener creado el plan de estudio, tener creado la evaluación de tiro para ese plan de estudio. El procedimiento debe distinguir si es bombero o no _~~_y de acuerdo a eso crear o no la inscripción a la evaluación de tiro del plan de estudio. (PREGUNTAR a P. Betanzo si es posible distinguir Bomberos con estado policial a los que no lo son)._~~_ Para determinar si es bombero con estado policial, el cae enviará un nuevocampo_\[GB2] \[GB3] _con ese dato._

2\)     habilite acceso al Moodle para acceso a material,

_**Importante**: se debe conocer el ID de el o los cursos de Moodle_\[GB4]&#x20;

3\)     ~~cree 2 contratos del efectivo con el nuevo plan de estudio, uno del período enero-junio, y otro del período julio-diciembre.~~ cree el contrato del efectivo con el nuevo plan de estudio, para el período que corresponda de acuerdo a la fecha del proceso de inscripción, (períodos enero-junio y julio-diciembre).

_**Importante**: cuando se grabe la asistencia al turno, se grabará en cada contrato del plan de estudio el aprobado, eso se utilizará el año posterior para corroborar que estuvo en las dos instancias._

***

**Recepción y asistencia**

Se necesita una interfaz para leer la asistencia al entrenamiento anual en el ISSP. Debe leer el DNI y grabar la confirmación del turno y el aprobado en el contrato del plan de estudio en el que corresponda de acuerdo a la fecha\[GB1] .

**Aplicación de tiro**

Se debe adaptar la aplicación de tiro para que grabe directamente en la base, se elimina la importación de turnos y la exportación de resultados. Hablar con Mariano\[GB2]&#x20;

**Reasignación de turno de entrenamiento**

Armar método de webservices para permitir reasignar turnos de entrenamiento\[GB3] .

**Devolución de asistencia al entrenamiento anual\[GB4]**&#x20;

Armar método de webservices para devolver asistencia al entrenamiento anual de acuerdo al nuevo esquema.

**Reasignación de turnos de examen de ascenso\[GB5]**&#x20;

Armar método de webservices para permitir reasignar turnos de examen de ascenso.

**Reasignación de comisiones de ascenso\[GB6]**&#x20;

Armar método de webservices para permitir reasignar comisiones de ascenso.

***
