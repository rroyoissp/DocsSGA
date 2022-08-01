# TIPS Certificados Seguridad Privada

### Historia de Revisiones del Documento

14/03/2022 - Gabriel Benitez - Creación del documento

### Problemática

Describir tips para sacar certificados por fuera del circuito cuando no se generaron por algún error.

### Contenidos

1\) Buscar el registro que corresponde al alumno y curso en la tabla SEGPRIV\_CursoPersona

2\) Grabar la nota ejecutando el sp SEGPRIV\_GrabarNota pasando los parámetros correctos, por ejemplo

`set @SegPrivCursoPersonaId = 8596`

`set @Nota = 9`

`set @Aprobado = 1`

`set @FechaExamen = '20220110'`

3\) Copiar codigo resultante (QR) y pegarlo en el codigo embebido de la página TestWebServices.aspx en el codebehind de la línea 25 dentro del proyecto Techmind.Adiutor.GUI y carpeta SeguridadPrivada. Ejemplo:

`string token = "016E9EFD-135C-49A8-81EB-CC36A68593C2";`

&#x20;También cambiar el nombre del archivo a generar en la línea 20 poniendo el nro de dni correspondiente. Ejemplo:

`string nombreArchivo = path + "24869524_QR.png"`

&#x20;4\) Copiar el archivo de imagen QR generado en la carpeta que se indica en la línea 19 y pegarlo en el servidor donde esta publicado SGA

&#x20; \\\10.26.250.106\Webs\instituto\Uploads\Archivos&#x20;

5\) Modificar temporalmente el sp RPT\_SEGPRIV\_ObtenerDatosCertificado, sacando comentario de la línea donde se establece la ruta del archivo

`select @Path = 'C:\Webs\instituto\Uploads\Archivos\`

6\) Loguearse al SGA como administrador o usuario con permisos para ejecutar el reporte "Certificado Seg Priv 1 Firma" que está en el catálogo Certificados y generarlo como pdf colocando el id obtenido en punto 1

7\) Descargar el archivo y cambiar su nombre a DNI\_Id\_CertSegPriv.pdf, por ejemplo 24869524\_8596\_CertSegPriv.pdf y pegarlo en carpeta del punto 4

8\) Copiar el archivo de imagen del qr y el pdf generado al servidor 10.26.250.233 carpeta C:\Servicios\ISSP\_WormHole\Archivos y ejecutar archivo .bat mueve\_archivos\_FS

9\) Cambiar el estado del archivo SegPrivCursoPersona segun corresponda a la siguiente lista

```
strStatus(1) = "No Inició"
strStatus(2) = "Cursando"
strStatus(3) = "Fin Cursada"
strStatus(4) = "Agendado E1"
strStatus(5) = "Cancelado E1"
strStatus(6) = "ReAgendado E1"
strStatus(7) = "Ausente El"
strStatus(8) = "Rindio Mal E1"
strStatus(9) = "Agendado E2"
strStatus(10) = "Cancelado E2"
strStatus(11) = "ReAgendado E2"
strStatus(12) = "Ausente E2"
strStatus(13) = "Rindio Mal E2"
strStatus(14) = "Aprobado E1"
strStatus(15) = "Aprobado E2"
strStatus(16) = "Recursar"
update SEGPRIV_CursoPersona set Status=14 where SEGPRIV_CursoPersonaID=8596
```

10\) volver atras la modificacion en el sp del punto 5, comentando la linea.

11\) probar descargar el certificado desde srvcalendar: https://srvcalendar.insusep.edu.ar/?CUIT=01234567890\&Tipo=0

12\) Borrar los archivos del servidor que se copiaron en punto 4 y 7
