# PEP Descripción

### Historia de Revisiones del Documento

18/03/2022 - Gabriel Benitez - Creación del documento

### Problemática

Describir el circuito para PEP, indicando sistemas e interfaces intervinientes.

## Contenidos

El Plan de Evaluación Permanente, de acá en más PEP, consta de 6 etapas obligatorias y 1 opcional:

1\) **Obtener y procesar turnos.** En esta etapa se utiliza el SGA, accediendo a la interfaz “PEP - Ascenso / Procesar Inscriptos” (_PEA/PEP\_ProcesarInscriptos_). El proceso está descripto en el documento “FUNC-Procesar Inscriptos PEP.docx”

2\) **Recepción del personal.** También el SGA se encuentra la interfaz para recepción, “PEP - Ascenso / Recepción Examenes” (_PEA/PEP\_Recepcionv2.aspx_). En esta interfaz se lee el DNI con las lectoras o se ingresa el número manualmente y el sistema valida el turno (sp PEP\_VALIDAR), si existe muestra el botón “Inscribir” que al presionarlo realiza las siguientes acciones: &#x20;

1\.      Obtiene la jerarquía

2\.      Busca el examen de Moodle relacionado a la jerarquía, en la tabla JerarquiaPCBAExamen.

3\.      Si es Bombero Policía busca la jerarquía equivalente en JerarquiaPCBA.JerarquiaPCBAIDEquivalente, obtiene JerarquiaPCBAExamen.MoodleCourseExamenId y lo inscribe en la plataforma Moodle que corresponda según JerarquiaPCBAExamen.OpcionMoodle con ese ID, si no tiene valor en ese campo inscribe como en punto 3.\[GB1]&#x20;

4\.      Si es Policía o Bombero Civil obtiene JerarquiaPCBAExamen.MoodleCourseExamenId y lo inscribe en la plataforma Moodle que corresponda según JerarquiaPCBAExamen.OpcionMoodle.

Para inscribir utiliza el método Moodles\_Utiles.InscribirAlumnoEnCurso (que usa varios métodos del webservice de Moodle). Luego de inscribirlo, actualiza el password del alumno en Moodle con la clave generada y guardada en la tabla SystemaParameters, campo CLAVEEXAMENMOODLE (ver 7 - Generación de clave aleatoria).

3\) **Impresión de exámenes y grabación de Notas de Protocolo.** En el SGA se encuentra la interfaz “Moodle / Impresión de Exámenes“ (_Moodle/ImpresionExamenesGrilla.aspx_)  , en esta pantalla se listan los turnos que fueron recibidos en el día en la interfaz del punto 2 y permite seleccionarlos e imprimir el examen, esta acción de imprimir también graba el resultado en nuestra base de datos, en la tabla MoodleExamenCabecera y MoodleExamenDetalle. A continuación describimos los pasos que se realizan en este punto:

a)      Obtiene la jerarquía de la table TiroLegajo, sino la encuentra devuelve un mensaje de error.

b)     Obtiene el registro de resultados del día de la tabla PEPDiaria, sino lo encuentra devuelve un mensaje de error.

c)      Obtiene el examen de Moodle y el ID de QUIZ (MoodleQuizId) o Cuestionario correspondiente a la jerarquía de la tabla JerarquiaPCBAExamenMoodle, sino los encuentra no continúa.

d)     Obtiene el usuario de Moodle a partir del número de documento que es el nombre de usuario en la plataforma virtual, sino lo encuentra devuelve un mensaje de error.

e)     Valida si es Bombero Policía y obtiene la jerarquía equivalente \[GB2] (JerarquiaPCBA.JerarquiaPCBAIDEquivalente), esto es debido a que los Bomberos Policías mantienen la jerarquía de policía. Busca la jerarquía equivalente y obtiene el ID de examen para esta jerarquía y obtiene las respuestas, DEBE ESTAR GUARDADA LA JERARQUIA EQUIVALENTE.  Sino es Bombero Policía directamente busca las respuestas para el examen de la jerarquía obtenida en punto c).

f)       Graba la cabecera del examen en MoodleExamenCabecera y las respuestas en MoodleExamenDetalle.

g)      Calcula la nota de acuerdo a cantidad de respuestas correctas y las graba en PEP\_Diaria en ProtocoloRespuestasOK, de acuerdo a esta nota graba en ProtocoloResultado DE (Desaprobado), AG (Apto Grado) y AA (Apto Ascenso) . DE = 0 a 3, AG = 4 a 6, AA = 7 a 10.\[GB3]&#x20;

h)     Imprime los exámenes de los seleccionados para imprimir, utilizando el reporte “moodleexamenes\_varios.rpt”

**4) Grabación de resultados de Educación física.** En la interfaz del SGA “PEP – Ascenso / Carga de Ed Física“ (_PEA/PEP\_EducacionFisica.aspx_)  se cargan los resultados de las pruebas físicas, se selecciona la fecha y el turno y el sistema devuelve la lista de alumnos con la posibilidad de carga de los ejercicios de acuerdo a la edad, Abdominales y Navette para menores de 50 y Marcha para mayores de \[GB4] 50. Para calcular los resultados utiliza el un Trigger de base de datos (_Pep\_diaria.tr\_ResultadoEdFisicaPepDiaria_) donde se definen los baremos para DE, AG y AA, de acuerdo a edad, sexo y resultados. Los resultados se graban en la tabla Pep\_Diaria: EdFIsica1, EdFisica2 y EdFisica3, el trigger se encarga de calcular el resultado y grabarlo en EdFisica\_Resultado \[GB5] (DE, AG y AA).

CASOS ESPECIALES:

**5) Grabación de resultados de Tiro.** Se utiliza la App de Tiro\[GB6] .

**6)** **Devolver resultados.** Para la devolución de resultados se deja disponible un método de servicio web llamado “ObtenerResultados” ([https://academico.insusep.edu.ar/WSpep/ServiciosPEP.asmx?op=ObtenerResultados](https://academico.insusep.edu.ar/WSpep/ServiciosPEP.asmx?op=ObtenerResultados) )

**NOTA**: Descripto en el documento FUNC-Especificación de Servicios Externos Disponibles PCBA PAE\_PEP\_v2.docx, utiliza el procedimiento almacenado “R_PT\_PEP\_Acta_”.

**7)** **Reasignar turnos para PEP (etapa OPCIONAL).** Para permitir la reasignación de turnos existe otro método en el servicio web denominado “ReasignacionTurno” ([https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op= ReasignacionTurno](https://academico.insusep.edu.ar/wspep/ServiciosPEP.asmx?op=AsignacionTurnoEntrenamiento))

***
