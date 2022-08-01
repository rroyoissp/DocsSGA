---
description: 04/10/2021 - Gabriel Benitez
---

# Imputación BUI



### **Historia de revisiones del documento**

04/10/2021 - Gabriel Benitez : Creación del documento\
03/03/2022 - Gabriel Benitez : Modificación para descripción / Imputación

### **Problemática**

El Sistema de Gestión Académica (SGA), gestiona las cuentas corrientes de los alumnos para las carreras pagas que dicta el ISSP. Los pagos se realizan a través de las Boletas Únicas Inteligentes (BUI) que son administradas por el departamento de Hacienda del Gobierno de la Ciudad. Se necesita imputar los pagos realizados a través de BUI en las cuotas generadas en el SGA para los contratos de las distintas carreras.

### **Relevamiento**

![](<.gitbook/assets/FUNC-Imputación BUI.png>)

### **Contenidos**

**SGA**

Proyecto: Techmind.Adiutor.GUI\
Página: Administrativo/Contrato/ImputacionBUI.aspx

**Servicios Web**

Proyecto: WSInsusep\
Servicio: ServiciosISSP.asmx

**Servicios WEB Hacienda**

[https://buisir.buenosaires.gob.ar/SERVICE/api/BUI/](https://buisir.buenosaires.gob.ar/SERVICE/api/BUI/)

### **Cómo se graba la Imputación BUI**

Una vez seleccionada una BUI para ser imputada el sistema sigue los siguientes pasos:

* Busca el alumno por el número de documento relacionado a la BUI.
* Busca los devengados impagos utilizando el procedimiento “TESO\_ObtenerDevengados”. Estos son los registros de la tabla AlumnoDevengado cuyo estado es “P” (Pendiente)
* Toma el primer registro impago (AlumnoDevengado.Estado=”P”) que no esté Anulado (AlumnoDevengado.FechaAnulado=null), no esté marcado como Beca (AlumnoDevengado.Beca=null) y sea del año corriente (AlumnoDevengado.Fecha.Año = Año actual)
* Se fija si ese registro tiene un formulario de pago asociado (InscripcionFormularioPago.AlumnoDevengadoId = AlumnoDevengado.AlumnoDevengadoId), si no lo tiene lo genera:



| Tabla.Campo                                  | Tipo de dato | Comentario                                            |
| -------------------------------------------- | ------------ | ----------------------------------------------------- |
| InscripcionFormularioPago.UsersId            | int          | Id del usuario logueado, se obtiene de la página base |
| InscripcionFormularioPago.Fecha              | datetime     | Fecha y hora actual                                   |
| InscripcionFormularioPago.AlumnoDevengadoId  | int          | Id del devengado (AlumnoDevengado)                    |
| InscripcionFormularioPago.FormularioCodigo   | varchar      | Nro de Boleta única inteligente (BUI)                 |
| **I**nscripcionFormularioPago.NroBoletaUnica | varchar      | Nro de Boleta única inteligente (BUI)                 |

* Imputa el pago con el proceso “PagarFormularioPago”, que es un proceso transaccionado que graba en las siguientes tablas y campos:

| Tabla.Campo                              | Tipo de dato | Comentario          |
| ---------------------------------------- | ------------ | ------------------- |
| InscripcionFormularioPago.FechaProcesado | datetime     | Fecha y hora actual |

Pago pago = new Pago { Fecha = DateTime.Now.Date, Importe = devengado.ImporteSaldo, Alumno = formulario.Alumno, UserEmitio = user };

| Tabla.Campo        | Tipo de dato  | Comentario                                                                          |
| ------------------ | ------------- | ----------------------------------------------------------------------------------- |
| Pago.Fecha         | datetime      | Fecha y hora actual                                                                 |
| Pago.Importe       | decimal(18,2) | Suma de AlumnoDevengadoDetalle.Importe menos la suma de PagoAlumnoDevengado.Importe |
| Pago.PersonaId     | int           | AlumnoDevengado.PersonaId                                                           |
| Pago.UsersIdEmitio | int           | Id del usuario logueado , se obtiene de la página base.                             |

| Tabla.Campo                           | Tipo de dato  | Comentario                              |
| ------------------------------------- | ------------- | --------------------------------------- |
| PagoAlumnoDevengado.PagoId            | int           | Id del pago, insertado en paso anterior |
| PagoAlumnoDevengado.AlumnoDevengadoId | int           | Id del Alumno Devenegado                |
| PagoAlumnoDevengado.Importe           | decimal(18,2) | Importe grabado en Pago (Pago.Importe)  |

| Tabla.Campo         | Tipo de dato  | Comentario                                                                                              |
| ------------------- | ------------- | ------------------------------------------------------------------------------------------------------- |
| Valor.Fecha         | datetime      | Fecha y hora actual                                                                                     |
| Valor.Importe       | decimal(18,2) | Importe de PagoAlumnoDevenegado(PagoAlumnoDevenegado.Importe)                                           |
| Valor.MedioPagoId   | int           | <p>Id del medio de pago, se obtiene del parámetro de sistema<br>(SystemParameters.MEDIAPAGODEFAULT)</p> |
| Valor.EstadoValorId | int           | Id del estado del valor, se obtiene del parámetro de sistema (SystemParameters. ESTADOVALORDEFAULT)     |

| Tabla.Campo       | Tipo de dato  | Comentario                                                            |
| ----------------- | ------------- | --------------------------------------------------------------------- |
| ValorPago.Fecha   | datetime      | Fecha y hora actual                                                   |
| ValorPago.Importe | decimal(18,2) | Importe grabado en PagoAlumnoDevenegado(PagoAlumnoDevenegado.Importe) |
| ValorPago.ValorId | int           | Id del Valor (Valor.ValorId)                                          |

| Tabla.Campo             | Tipo de dato | Comentario                                             |
| ----------------------- | ------------ | ------------------------------------------------------ |
| AlumnoDevenegado.Estado | varchar      | Se graba "G" para sacarlo del estado pendiente de pago |
