# Prácticas de AWS

Prácticas con AWS CLI sobre el principio de menor privilegio, el almacenamiento en Amazon S3 y el despliegue de un servidor web en Amazon EC2.

## Índice

- [Semana 1 · IAM y permisos de lectura de EC2](#semana-1)
- [Semana 2 · Almacenamiento en S3, roles de IAM y EC2](#semana-2)
  - [Ciclo de vida de un bucket en S3](#ciclo-de-vida-de-un-bucket-en-s3)
  - [Rol de IAM para una instancia EC2](#rol-de-iam-para-una-instancia-ec2)
  - [Servidor web en EC2 con acceso a S3](#servidor-web-en-ec2-con-acceso-a-s3)

## Semana 1

La práctica de IAM documenta la creación del usuario `dev-santiago`, su cambio de nombre a `lector-santiago` y la asignación de una política de lectura de EC2. Las pruebas muestran que el usuario puede consultar instancias de EC2, recibe un error al intentar listar usuarios de IAM y pierde el acceso a EC2 cuando se retira la política. La práctica termina con la eliminación de la llave de acceso y del usuario.

| Recurso | Contenido |
| --- | --- |
| [Resultado de la práctica de IAM](./iam/activity-result.md) | Transcripciones de los pasos y sus resultados. |
| [Capturas de IAM](./iam/evidencias/) | Evidencias de creación, cambios de permisos, pruebas y eliminación del usuario. |
| [Guía de IAM](./iam/01-info.md) | Conceptos y comandos de AWS CLI para usuarios, llaves de acceso, roles y políticas. |
| [Comandos de IAM](./iam/02-command.md) | Referencia de AWS CLI y comandos para probar los permisos del perfil lector. |
| [Enunciado de la actividad de IAM](./iam/03-activity.md) | Pasos del ciclo de vida de un usuario IAM y preguntas de reflexión. |

## Semana 2

### Ciclo de vida de un bucket en S3

La práctica de S3 documenta la creación de un bucket privado, la subida, consulta, actualización y descarga de objetos, y el uso de un enlace temporal. También prueba con un usuario lector que `s3:GetObject` permite leer un objeto y que listar o borrar objetos requiere permisos adicionales. La verificación final comprueba que se eliminaron el bucket y el usuario lector.

| Recurso | Contenido |
| --- | --- |
| [Información sobre S3](./s3-roles-ec2/s3/01-info.md) | Conceptos de buckets, objetos, claves y permisos. |
| [Comandos de S3](./s3-roles-ec2/s3/02-command.md) | Referencia de AWS CLI para los pasos de la práctica. |
| [Enunciado de la actividad](./s3-roles-ec2/s3/03-activity.md) | Objetivo, pasos y preguntas de reflexión. |
| [Evidencia y reflexión](./s3-roles-ec2/s3/evidencia.md) | Resultados, pruebas de acceso, limpieza y respuestas. |
| [Capturas de S3](./s3-roles-ec2/s3/capturas/) | Evidencias visuales de la actividad. |
| [Archivos de prueba](./s3-roles-ec2/s3/archivos/) | `notas.txt`, `tareas.txt` y `secreto.txt`, usados para las operaciones en el bucket. |
| [Descargas](./s3-roles-ec2/s3/descargas/) | Copia de `secreto.txt` descargada desde el bucket. |
| [Política de solo lectura](./s3-roles-ec2/s3/solo-lectura.json) | Permite `s3:GetObject` sobre los objetos del bucket de la práctica. |

### Rol de IAM para una instancia EC2

La práctica de Roles documenta la creación de `ec2-lector-s3`, la política en línea `leer-reportes` para leer objetos de `reportes-santiago-001` y la asociación del rol con su perfil de instancia. La evidencia incluye el error `DeleteConflict` al intentar borrar el rol mientras sigue en el perfil.

| Recurso | Contenido |
| --- | --- |
| [Guía de roles y perfiles de instancia](./s3-roles-ec2/roles/01-info.md) | Políticas de confianza, permisos y credenciales temporales para EC2. |
| [Comandos de roles](./s3-roles-ec2/roles/02-command.md) | Referencia de AWS CLI para roles, políticas y perfiles de instancia. |
| [Enunciado de Roles](./s3-roles-ec2/roles/03-activity.md) | Pasos de la práctica y preguntas de reflexión. |
| [Evidencia y reflexión de Roles](https://github.com/sntiago05/aws-actividades/blob/2f434f24f876b85262af7c66a1a6f4c3f02342df/semana-2/roles/evidencia.md) | Resultados respaldados por las capturas y respuestas a las cinco preguntas, en la revisión original. |
| [Capturas de Roles](./s3-roles-ec2/roles/files/imgs/) | Salidas de la práctica. El error al intentar eliminar el rol está en la revisión original enlazada arriba. |
| [Política de confianza](./s3-roles-ec2/roles/files/policies/confianza.json) | Permite que EC2 asuma el rol. |
| [Política de permisos](./s3-roles-ec2/roles/files/policies/permisos.json) | Permite `s3:GetObject` sobre los objetos del bucket de reportes. |
| [Archivo de prueba](./s3-roles-ec2/roles/files/reporte.txt) | `reporte.txt`, usado para la subida a S3. |

### Servidor web en EC2 con acceso a S3

La práctica de EC2 reúne la configuración de una instancia Amazon Linux 2023, un grupo de seguridad para HTTP y SSH y el perfil `ec2-lector-s3`. Las capturas muestran la respuesta de Apache desde la instancia, la lectura de `reporte.txt`, dos operaciones denegadas al rol y el cambio de IP pública después de detener y volver a iniciar la instancia.

| Recurso | Contenido |
| --- | --- |
| [Guía de EC2](./s3-roles-ec2/ec2/01-info.md) | Conceptos de instancias, red, seguridad y perfil de instancia. |
| [Comandos de EC2](./s3-roles-ec2/ec2/02-command.md) | Referencia de AWS CLI para lanzar, administrar y eliminar la instancia. |
| [Enunciado de EC2](./s3-roles-ec2/ec2/03-activity.md) | Pasos de la práctica y preguntas de reflexión. |
| [Evidencia y reflexión de EC2](./s3-roles-ec2/ec2/evidencia.md) | Capturas, salidas de terminal y respuestas a las seis preguntas. |
| [Capturas de EC2](./s3-roles-ec2/ec2/imgs/) | Evidencias desde la configuración inicial hasta la limpieza. |
| [Script de inicio](./s3-roles-ec2/ec2/scripts/inicio.sh) | Instala Apache y escribe la página que sirve la instancia. |
