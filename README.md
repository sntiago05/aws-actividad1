# Prácticas de AWS

Prácticas con AWS CLI sobre el principio de menor privilegio y el almacenamiento en Amazon S3.

## Índice

- [Semana 1 · IAM y permisos de lectura de EC2](#semana-1)
- [Semana 2 · Ciclo de vida de un bucket en S3](#semana-2)

## Semana 1

La práctica de IAM documenta la creación del usuario `dev-santiago`, su cambio de nombre a `lector-santiago` y la asignación de una política de lectura de EC2. Las pruebas muestran que el usuario puede consultar instancias de EC2, recibe un error al intentar listar usuarios de IAM y pierde el acceso a EC2 cuando se retira la política. La práctica termina con la eliminación de la llave de acceso y del usuario.

| Recurso | Contenido |
| --- | --- |
| [Resultado de la práctica de IAM](./semana-1/activity-result.md) | Transcripciones de los pasos y sus resultados. |
| [Capturas de IAM](./semana-1/evidencias/) | Evidencias de creación, cambios de permisos, pruebas y eliminación del usuario. |
| [Guía de IAM](./semana-1/01-info.md) | Conceptos y comandos de AWS CLI para usuarios, llaves de acceso, roles y políticas. |
| [Enunciado de la actividad de IAM](./semana-1/03-activity.md) | Pasos del ciclo de vida de un usuario IAM y preguntas de reflexión. |

## Semana 2

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
