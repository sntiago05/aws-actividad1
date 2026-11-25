# Prácticas de AWS

Prácticas con AWS CLI sobre el principio de menor privilegio y el almacenamiento en Amazon S3.

## Índice

- [Semana 1 · IAM y permisos de lectura de EC2](#semana-1)
- [Semana 2 · Almacenamiento en S3 y roles de IAM](#semana-2)
  - [Ciclo de vida de un bucket en S3](#ciclo-de-vida-de-un-bucket-en-s3)
  - [Rol de IAM para una instancia EC2](#rol-de-iam-para-una-instancia-ec2)

## Semana 1

La práctica de IAM documenta la creación del usuario `dev-santiago`, su cambio de nombre a `lector-santiago` y la asignación de una política de lectura de EC2. Las pruebas muestran que el usuario puede consultar instancias de EC2, recibe un error al intentar listar usuarios de IAM y pierde el acceso a EC2 cuando se retira la política. La práctica termina con la eliminación de la llave de acceso y del usuario.

| Recurso | Contenido |
| --- | --- |
| [Resultado de la práctica de IAM](./semana-1/activity-result.md) | Transcripciones de los pasos y sus resultados. |
| [Capturas de IAM](./semana-1/evidencias/) | Evidencias de creación, cambios de permisos, pruebas y eliminación del usuario. |
| [Guía de IAM](./semana-1/01-info.md) | Conceptos y comandos de AWS CLI para usuarios, llaves de acceso, roles y políticas. |
| [Comandos de IAM](./semana-1/02-command.md) | Referencia de AWS CLI y comandos para probar los permisos del perfil lector. |
| [Enunciado de la actividad de IAM](./semana-1/03-activity.md) | Pasos del ciclo de vida de un usuario IAM y preguntas de reflexión. |

## Semana 2

### Ciclo de vida de un bucket en S3

La práctica de S3 documenta la creación de un bucket privado, la subida, consulta, actualización y descarga de objetos, y el uso de un enlace temporal. También prueba con un usuario lector que `s3:GetObject` permite leer un objeto y que listar o borrar objetos requiere permisos adicionales. La verificación final comprueba que se eliminaron el bucket y el usuario lector.

| Recurso | Contenido |
| --- | --- |
| [Información sobre S3](./semana-2/s3/01-info.md) | Conceptos de buckets, objetos, claves y permisos. |
| [Comandos de S3](./semana-2/s3/02-command.md) | Referencia de AWS CLI para los pasos de la práctica. |
| [Enunciado de la actividad](./semana-2/s3/03-activity.md) | Objetivo, pasos y preguntas de reflexión. |
| [Evidencia y reflexión](./semana-2/s3/evidencia.md) | Resultados, pruebas de acceso, limpieza y respuestas. |
| [Capturas de S3](./semana-2/s3/capturas/) | Evidencias visuales de la actividad. |
| [Archivos de prueba](./semana-2/s3/archivos/) | `notas.txt`, `tareas.txt` y `secreto.txt`, usados para las operaciones en el bucket. |
| [Descargas](./semana-2/s3/descargas/) | Copia de `secreto.txt` descargada desde el bucket. |
| [Política de solo lectura](./semana-2/s3/solo-lectura.json) | Permite `s3:GetObject` sobre los objetos del bucket de la práctica. |

### Rol de IAM para una instancia EC2

La práctica de Roles documenta la creación de `ec2-lector-s3`, la política en línea `leer-reportes` para leer objetos de `reportes-santiago-001` y la asociación del rol con su perfil de instancia. La evidencia incluye el error `DeleteConflict` al intentar borrar el rol mientras sigue en el perfil.

| Recurso | Contenido |
| --- | --- |
| [Guía de roles y perfiles de instancia](./semana-2/roles/01-info.md) | Políticas de confianza, permisos y credenciales temporales para EC2. |
| [Comandos de roles](./semana-2/roles/02-command.md) | Referencia de AWS CLI para roles, políticas y perfiles de instancia. |
| [Enunciado de Roles](./semana-2/roles/03-activity.md) | Pasos de la práctica y preguntas de reflexión. |
| [Evidencia y reflexión de Roles](./semana-2/roles/evidencia.md) | Resultados respaldados por las capturas y respuestas a las cinco preguntas. |
| [Capturas de Roles](./semana-2/roles/files/imgs/) | Salidas de la práctica y error al intentar eliminar el rol. |
| [Política de confianza](./semana-2/roles/files/policies/confianza.json) | Permite que EC2 asuma el rol. |
| [Política de permisos](./semana-2/roles/files/policies/permisos.json) | Permite `s3:GetObject` sobre los objetos del bucket de reportes. |
| [Archivo de prueba](./semana-2/roles/files/reporte.txt) | `reporte.txt`, usado para la subida a S3. |
