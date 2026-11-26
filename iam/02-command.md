# Comandos de IAM con AWS CLI

Consulta la [guía de IAM](./01-info.md) y el [enunciado de la práctica](./03-activity.md).

## Identidad

| Comando | Qué hace |
| --- | --- |
| `aws sts get-caller-identity` | Muestra con qué identidad estoy conectado |
| `aws configure get region` | Muestra la región configurada |

## Usuarios

| Comando | Qué hace |
| --- | --- |
| `aws iam create-user --user-name <usuario>` | Crea un usuario |
| `aws iam list-users` | Lista todos los usuarios |
| `aws iam get-user --user-name <usuario>` | Muestra los datos de un usuario |
| `aws iam tag-user --user-name <usuario> --tags Key=area,Value=desarrollo` | Agrega una etiqueta al usuario |
| `aws iam update-user --user-name <usuario> --new-user-name <nombre-nuevo>` | Cambia el nombre del usuario |
| `aws iam attach-user-policy --user-name <usuario> --policy-arn <arn>` | Le adjunta una política al usuario |
| `aws iam list-attached-user-policies --user-name <usuario>` | Lista las políticas del usuario |
| `aws iam detach-user-policy --user-name <usuario> --policy-arn <arn>` | Le quita una política al usuario |
| `aws iam delete-user --user-name <usuario>` | Borra el usuario (sin políticas ni llaves) |

## Llaves de acceso

| Comando | Qué hace |
| --- | --- |
| `aws iam create-access-key --user-name <usuario>` | Crea una llave de acceso para el usuario |
| `aws iam list-access-keys --user-name <usuario>` | Lista las llaves del usuario |
| `aws iam delete-access-key --user-name <usuario> --access-key-id <id>` | Borra una llave |

## Roles

| Comando | Qué hace |
| --- | --- |
| `aws iam create-role --role-name <rol> --assume-role-policy-document file://confianza.json` | Crea un rol con su política de confianza |
| `aws iam list-roles` | Lista todos los roles |
| `aws iam get-role --role-name <rol>` | Muestra los datos de un rol |
| `aws iam put-role-policy --role-name <rol> --policy-name <nombre> --policy-document file://permisos.json` | Le da permisos al rol (política en línea) |
| `aws iam list-role-policies --role-name <rol>` | Lista las políticas en línea del rol |
| `aws iam get-role-policy --role-name <rol> --policy-name <nombre>` | Muestra el contenido de una política del rol |
| `aws iam delete-role-policy --role-name <rol> --policy-name <nombre>` | Borra una política del rol |
| `aws iam delete-role --role-name <rol>` | Borra el rol (sin políticas ni perfil) |

## Perfiles de instancia

| Comando | Qué hace |
| --- | --- |
| `aws iam create-instance-profile --instance-profile-name <nombre>` | Crea un perfil de instancia |
| `aws iam add-role-to-instance-profile --instance-profile-name <nombre> --role-name <rol>` | Mete el rol dentro del perfil |
| `aws iam list-instance-profiles` | Lista los perfiles de instancia |
| `aws iam get-instance-profile --instance-profile-name <nombre>` | Muestra un perfil y el rol que contiene |
| `aws iam remove-role-from-instance-profile --instance-profile-name <nombre> --role-name <rol>` | Saca el rol del perfil |
| `aws iam delete-instance-profile --instance-profile-name <nombre>` | Borra el perfil |

## Políticas administradas por AWS

| Comando | Qué hace |
| --- | --- |
| `aws iam list-policies --scope AWS --max-items 20` | Lista políticas ya hechas por AWS |
| `aws iam get-policy --policy-arn <arn>` | Muestra los datos de una política |

## Trucos para leer la salida

| Opción | Qué hace |
| --- | --- |
| `--output table` | Muestra la respuesta como tabla en vez de JSON |
| `--query "Roles[].RoleName"` | Filtra la respuesta y deja solo lo que pides |
| `aws iam <comando> help` | Muestra la ayuda de cualquier comando |

## Perfil lector y prueba de permisos

| Comando | Qué hace |
| --- | --- |
| `aws configure --profile lector` | Configura el perfil de la práctica. |
| `aws sts get-caller-identity --profile lector` | Confirma la identidad asociada al perfil. |
| `aws ec2 describe-instances --profile lector` | Consulta las instancias de EC2 con los permisos del perfil. |
| `aws iam list-users --profile lector` | Prueba si el perfil puede listar usuarios de IAM. |

## Orden para borrar

IAM no deja borrar algo que todavía está en uso. El orden es el inverso al de creación:

1. Sacar el rol del perfil de instancia y borrar el perfil.
2. Borrar las políticas del rol y luego el rol.
3. Quitar políticas y llaves del usuario y luego borrar el usuario.
