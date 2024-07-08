`docker --version`: comprobar la versión.  
`docker version`: información de las versiones de los componentes.  
`docker info`: información del sistema que instalado.  
`docker run image [echo 'command']`: crea y corre un contenedor basado en la imagen que indicamos en `image`. En caso de ser necesario podemos indicerle también el comando a utilizar.   
`docker ps`: lista los contenedores que se están ejecutando.
* Opciones:
    * `-a`: lista los contenedores que **NO** se están ejecutando.

`docker rm [CONTAINER_ID | NAME]`: elimina el conetenedor que indiquemos ya sea por su **id** o por su **name**.  
`docker create image`: **SOLO** crea un contenedor basado en la imagen `image` pero **NO** lo inicia.  
`docker start name_container`: inicia la ejecución del contenedor `name_container`.  
* Opciones:
    * `-a`: nos permite conectar a la salida estándar del contenedor y poder ver en nuestro terminal la salida.
`docker images`: nos muestra la lista de imágenes que tenemos en nuestra registro local.  
`docker pull image`: descarga la imagen `image`de Docker Hub.
`docker rename old_name new_name`: renombrar el nombre del contenedor `old_name` a `new_name`.
`docker images ls`: nos muestra la lista de imágenes que tenemos en nuestra registro local.
`docker images list`: nos muestra la lista de imágenes que tenemos en nuestra registro local.
`docker events`: para ver las distintas etapas por las que pasa la creación de un contenedor. Lo ejecutamos en una terminal, y en otra ejecutamos el contenedor. En la terminal que hemos ejectuado el comando nos aparecerán las operaciones que se han producido.
