# Consultas utilizadas en la toma de ausentismo en SGA

#### Cursos del profesor (usuario logueado)

`select distinct c.CursoID as CursoId, c.Nombre as CursoNombre, m.MateriaID as MateriaId, m.Descripcion as MateriaDescripcion from CronogramaClaseProfesor ccp inner join CronogramaClase cc on ccp.CronogramaClaseID = cc.CronogramaClaseID inner join curso c on c.CursoID = cc.CursoID inner join materia m on m.MateriaID = c.MateriaID inner join persona p on p.personaId = ccp.personaId where p.usersId = 1838 and year(cc.FechaDesde) = '2021' and month(cc.FechaDesde) = '5' and day(cc.FechaDesde) = '11'`

#### Lista de Alumnos para la toma de ausentismo del curso

```
select cc.CronogramaClaseID,
	p.PersonaID, p.DocumentoNumero, p.Apellido, p.Nombre
	, cc.FechaDesde, pa.PresentismoAlumnoID,
	pa.CronogramaClaseID, pa.CursoID, pa.Detalle, pa.Fecha, pa.FechaRegistro,pa.Justificar,
	case when pa.PresenteAusente = 'A' then 1 else 0 end Ausente,
	ci.FechaBaja,
	ci.CursoInscripcionID,
	cc.FechaCargaPresentismo,
	licencias.*
	from CursoInscripcion ci inner join Persona p on ci.PersonaID = p.PersonaID
								inner join CronogramaClase cc on cc.CursoID = ci.CursoID
								inner join Curso cu on ci.CursoID = cu.CursoID
								left join PresentismoAlumno pa on cc.CronogramaClaseID = pa.CronogramaClaseID and ci.personaid=pa.personaid
								left join (select pl.*, t.Descripcion, t.Codigo from PersonaLicencia pl 
												inner join TipoLicencia t on pl.TipoLicenciaId = t.TipoLicenciaId where @Fecha between pl.FechaDesde and pl.FechaHasta) licencias on licencias.PersonaID = p.PersonaID
	where ci.CursoID=@CursoId -- 16601
	and year(cc.fechadesde) = year(@fecha)
	and month(cc.fechadesde) = month(@fecha)
	and day(cc.fechadesde) = day(@fecha)

```

#### Grabar el Ausente

Se graba en la tabla PresentismoAlumno:

| Campo                                | Valor a grabar                                       |
| ------------------------------------ | ---------------------------------------------------- |
| PresentismoAlumno.CronogramaClaseId  | CronogramaClaseId (está en query del punto 2)        |
| PresentismoAlumno.PersonaId          | Id de Persona del Alumno                             |
| PresentismoAlumno.FechaRegistro      | Fecha y Hora actual                                  |
| PresentismoAlumno.PresenteAusente    | "A"                                                  |
| PresentismoAlumno.UserIdentification | Identification del Usuario (string, no guarda el id) |

Si se vuelve atrás el ausente que se cargó, se debe eliminar el registro de la tabla. Recordar que graba los AUSENTES.

#### Cerrar Asistencia

Implica no poder volver a tocar el ausentismo de esta clase.\
``Se graba en la tabla CronogramaClase, campo FechaCargaPresentismo el fecha y hora al momento de cerrar la asistencia.
