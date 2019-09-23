# aws-pipeline-codebuild

Este tutorial permite hacer un deploy desde github a AWS S3.
Sirve para una App en react (usé create-react-app).
Usa:
- CodePipeline: para traer el codigo desde github.
- CodeBuild: para hacer el build y deployarlo en el bucket de s3.

NO USO: codepipeline para tirar el codigo en s3 (lo soluciono con Codebuild).
NO SIRVE: si se usa server side rendering.


1- Crear pipeline de codigo (Desde consola de AWS).
Almacén de artefactos: "Ubicación predeterminadda". 
Clave de cifrado: "Predeterminada por AWS"

2- Elegir Github o el que sea. El repositorio y la rama, yo puse master.
Usar webhooks de Github. 

3- Proveedor de compilación:
AWS Codebuild.
Creo un proyecto nuevo (de Codebuild) con las siguientes configuraciones:

- Imagen del entorno: imagen administrada
- sistema operativo: Amazon Linux 2
- Tipo de ejecición: Standar
- Imagen: la que te propone el select.
- Versión de la imagen: opcion "Utilizar siempre la imagen más...".
- Privilegiado: NO marcar esta opcioón.
- nombre de rol: el que quieras.
- En Especificacion de compilación poner "Insertar comandos de compilación", apretar en el botón de "cambiar el editor" y poner:

ver archivo buildspect.yml

Acordarse de poner el nombre del bucket s3 donde se va a tirar el codigo.



4- Deshabilitar la transición de Build a Deploy. (o eliminarla, a esto no lo probé).

## Errores posibles

1- Cuando hace el Build da error en la parte POST_BUILD y dice algo de access denied cuando hace el putObject a s3:
  Para solucionar esto solo hay que buscar el Rol IAM y darle permiso Full en S3.


