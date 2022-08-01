---
description: >-
  09/11/2021 - Documento de Especificación de Web Services para la Integración
  con el Sistema de Gestión Académica del ISSP y el circuito de Cursos de
  Seguridad Privada
---

# Web Services del SGA aplicado al circuito de cursos de Seguridad Privada

### Especificación de Servicios Externos Disponibles

#### Obtener ID de una Boleta Única Inteligente a partir de su número

Devuelve el ID (GUID) de una BUI a partir de un número pasado como parámetro. _Utiliza la API de Hacienda_.\
\
_**Invocación**_\
****Se debe invocar mediante GET la sig. URL:\
[**https://academico.insusep.edu.ar/wssegprivada/ServiciosSegPriv.asmx?op=GetIdByNroBUI**](https://academico.insusep.edu.ar/wssegprivada/ServiciosSegPriv.asmx?op=GetIdByNroBUI)****\
****_**Parámetros**_\
****NroBui = en formato ####-######## (ejemplo: 2153-00000622)\
_**Respuesta**_\
****Este es un ejemplo de respuesta al método GetIdByNroBUI:\
****`<string xmlns="http://tempuri.org/">308ccd15-b966-4990-9df7-97c8d1cfb483</string>`

#### Obtener si un alumno está habilitado para rendir examen de Seguridad PrivadaObtener si un alumno está habilitado para rendir examen de Seguridad Privada

En la respuesta devuelve un SI en caso de estar habilitado para dar el examen o un NO, en caso contrario. No está habilitado si el alumno no está inscripto al curso, si no se encontró la BUI relacionada a la inscripción, si la BUI no está paga o si el alumno no completo el 100% de los cursos en la plataforma virtual. _Utiliza servicios webs de Moodle._\
__\
_**Invocación**_\
****Se debe invocar mediante POST la sig. URL:\
[**https://academico.insusep.edu.ar/wssegprivada/ServiciosSegPriv.asmx?op=SegPriv\_AlumnoHabilitadoParaExamen**](https://academico.insusep.edu.ar/wssegprivada/ServiciosSegPriv.asmx?op=SegPriv\_AlumnoHabilitadoParaExamen)****\
****_**Parámetros**_\
****personaId: es un entero (PersonaId de la tabla Persona)\
cursoId: es un entero (SegPriv\_CursoId de la tabla SEGPRIV\_Curso)\
****_**Respuesta**_\
Este es un ejemplo de respuesta al método SegPriv\_AlumnoHabilitadoParaExamen:\
`<string xmlns="http://tempuri.org/">NO</string>`

#### Obtener BUIs por contribuyente

Devuelve una o varias BUIs correspondientes a un contribuyente. _Utiliza la API de Hacienda_.\
\
**Invocación**\
[https://academico.insusep.edu.ar/wssegprivada/ServiciosSegPriv.asmx?op=SegPriv\_BoletasPorContribuyente](https://academico.insusep.edu.ar/wssegprivada/ServiciosSegPriv.asmx?op=SegPriv\_BoletasPorContribuyente)\
**Parámetros**\
CuitDni: en formato ######## o ########### si pasamos dni o cuit respectivamente.\
**Respuesta**\
Este es un ejemplo de respuesta al método SegPriv\_BoletasPorContribuyente:\
`<BoletasBUI xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://tempuri.org/">`\
`<Boletas/>`\
`<Total>0</Total>`\
`</BoletasBUI>`\
``\
``_**`Ó`**_

```
<Boletas>
<BoletaBUI>
<ID>e0ae0d11-fc85-4e1e-96c2-35dcf8b5deba</ID>
<Numero>2153-00000693</Numero>
<DependenciaID>db8009cf-d6ee-6344-9bac-cd612479d6f8</DependenciaID>
<Dependencia>
<ID>db8009cf-d6ee-6344-9bac-cd612479d6f8</ID>
<Nombre>Instituto Superior de Seguridad Pública</Nombre>
<Codigo>53</Codigo>
<Items/>
</Dependencia>
<Contribuyente>
<ID>fa28b5e1-1318-4d20-a29e-adda00b8db64</ID>
<TipoPersona>juridica</TipoPersona>
<TipoDocumento>
<ID>54a1409e-409f-f94f-93dc-88d86e39f425</ID>
<Codigo>CUIT</Codigo>
<Descripcion>Clave Unica de Identificacion Tributaria</Descripcion>
<Regex>^\d{9,11}$</Regex>
<Formato>CUIT</Formato>
</TipoDocumento>
<Documento>30523163171</Documento>
<Nombre>COMAHUE SEGURIDAD PRIVADA SA</Nombre>
<Direccion>Melo, Carlos F. 428</Direccion>
<Piso>PB</Piso>
<Departamento xsi:type="xsd:string">N/A</Departamento>
<Localidad>Ciudad Autónoma de Buenos Aires</Localidad>
<CodigoPostal>1163</CodigoPostal>
<Fecha>0001-01-01T00:00:00</Fecha>
<Email>habilitaciones@comahueseguridad.com.ar</Email>
<DocumentoTipoNumero>CUIT 30-52316317-1</DocumentoTipoNumero>
</Contribuyente>
<Fecha>2021-11-08T11:13:02</Fecha>
<Vencimiento>2021-11-11T23:59:59</Vencimiento>
<Conceptos>
<Concepto>
<ID>0c894212-31c5-4ead-9325-adda00b8db64</ID>
<ItemID>07ac495a-1cbe-4042-821f-22d497c3e3db</ItemID>
<Codigo>47.02.13</Codigo>
<Descripcion>Derecho de certif. técnico habilitante inicial para los agentes comprendidos en el art. 439 inc. 2) a. y 2) c., de la Ley N° 5.688</Descripcion>
<Cantidad>4</Cantidad>
<Importe>1070</Importe>
<Vigencia>0</Vigencia>
<DetalleValueToRules>0</DetalleValueToRules>
</Concepto>
</Conceptos>
<UsuarioID xsi:type="xsd:string">8db098eb-b8cc-ba43-b330-0935c201d0b7</UsuarioID>
<Usuario xsi:type="xsd:string">esalas</Usuario>
<UsuarioLegajo>16454501</UsuarioLegajo>
<UsuarioNombre xsi:type="xsd:string">Eduardo Adolfo </UsuarioNombre>
<Total>4280</Total>
<Estado>Pagada</Estado>
<CodBarras>E0AE0D11FC854E1E96C235DCF8B5DEBA470000069300004280001111210</CodBarras>
<Cancelado xsi:type="xsd:string"/>
<Anulado xsi:type="xsd:string"/>
<AplicaRedondeo>false</AplicaRedondeo>
<CodPERevisado>false</CodPERevisado>
<UltimoEstado xsi:type="xsd:string">Pagada</UltimoEstado>
<UltimoEstadoActualizadoFecha xsi:type="xsd:string">08/11/2021</UltimoEstadoActualizadoFecha>
</BoletaBUI>
<Total>1</Total>
</BoletasBUI>
```

#### Obtener Boletas (BUIs) por rango de fechas

Devuelve una o más boletas (BUIs) generadas entre fechas. _Utiliza la API de Hacienda_.\
\
_**Invocación**_\
Se debe invocar mediante POST la sig. URL:\
[**https://academico.insusep.edu.ar/wssegprivada/ServiciosSegPriv.asmx?op=SegPriv\_BoletasPorFecha**](https://academico.insusep.edu.ar/wssegprivada/ServiciosSegPriv.asmx?op=SegPriv\_BoletasPorFecha)\
_**Parámetros**_\
fechaDesde: en formato YYYY-MM-DD (Ejemplo: 2021-11-01)\
fechaHasta: en formato YYYY-MM-DD (Ejemplo: 2021-11-02)\
_**Respuesta**_\
Este es un ejemplo de respuesta al método SegPriv\_BoletasPorFecha:

```
<BoletasBUI xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://tempuri.org/">
<Boletas>
<BoletaBUI>
<ID>8f400002-a554-42a0-abbf-542986f232bb</ID>
<Numero>2153-00000619</Numero>
<DependenciaID>db8009cf-d6ee-6344-9bac-cd612479d6f8</DependenciaID>
<Dependencia>
<ID>db8009cf-d6ee-6344-9bac-cd612479d6f8</ID>
<Nombre>Instituto Superior de Seguridad Pública</Nombre>
<Codigo>53</Codigo>
<Items/>
</Dependencia>
<Contribuyente>
<ID>e458c736-9024-4ee2-8194-add300f7a9fc</ID>
<TipoPersona>fisica</TipoPersona>
<TipoDocumento>
<ID>a3853f0e-6da5-4949-870f-d2248b0d80d7</ID>
<Codigo>DNI</Codigo>
<Descripcion>Documento Nacional de Identidad</Descripcion>
<Regex>^\d{6,8}$</Regex>
<Formato>DNI</Formato>
</TipoDocumento>
<Documento>43239289</Documento>
<Nombre>Luana Aylen Martinez</Nombre>
<Direccion>2 DE ABRIL DE 1982 6873 </Direccion>
<Localidad>Ciudad de Buenos Aires</Localidad>
<CodigoPostal>1439</CodigoPostal>
<Fecha>0001-01-01T00:00:00</Fecha>
<Email>aylen.8@live.com.ar</Email>
<DocumentoTipoNumero>DNI 43.239.289</DocumentoTipoNumero>
</Contribuyente>
<Fecha>2021-11-01T15:01:42</Fecha>
<Vencimiento>2021-11-04T23:59:59</Vencimiento>
<Conceptos>
<Concepto>
<ID>6caa7197-8344-4437-9744-add300f7a9fc</ID>
<ItemID>897122f0-361c-4fa4-ac75-ffa515de829d</ItemID>
<Codigo>47.01.06</Codigo>
<Descripcion>Cuota Soporte Didáctico Tecnicaturas Superiores</Descripcion>
<Cantidad>1</Cantidad>
<Importe>4150</Importe>
<Vigencia>0</Vigencia>
<DetalleValueToRules>0</DetalleValueToRules>
</Concepto>
</Conceptos>
<UsuarioID xsi:type="xsd:string">52fe4314-2098-ff39-e053-e202490ad8d4</UsuarioID>
<Usuario xsi:type="xsd:string">portaltramites</Usuario>
<UsuarioLegajo>99150421</UsuarioLegajo>
<UsuarioNombre xsi:type="xsd:string">PortalTramites</UsuarioNombre>
<Total>4150</Total>
<Estado>Pagada</Estado>
<CodBarras>8F400002A55442A0ABBF542986F232BB470000061900004150000411212</CodBarras>

<Cancelado xsi:type="xsd:string"/>
<Pagado xsi:type="xsd:string">03/11/2021</Pagado>
<Anulado xsi:type="xsd:string"/>
<AplicaRedondeo>false</AplicaRedondeo>
<Traza xsi:type="xsd:string">86b03ab4-0d3d-42d7-9ee4-6ee7adb4fa88</Traza>
<CodPERevisado>false</CodPERevisado>
<UltimoEstado xsi:type="xsd:string">Pagada</UltimoEstado>
<UltimoEstadoActualizadoFecha xsi:type="xsd:string">04/11/2021</UltimoEstadoActualizadoFecha>
</BoletaBUI>
</Boletas>
<Total>1</Total>
</BoletasBUI>

```
