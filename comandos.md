`docker --version`: comprobar la versión.  
`docker version`: información de las versiones de los componentes.  
`docker info`: información del sistema que instalado.  
`docker run [echo 'command']`: crea y corre un contenedor basado en la imagen que indicamos en `image`. En caso de ser necesario podemos indicerle también el comando a utilizar.  
* Opciones:
    * `--name name_container`: para indicarle el nombre del contenedor.
    * `-h hostname_cointainer`: para indicarle el hostname.
    * `-i`: para abrir una sesión interactiva.
    * `-t`: nos permite crear un pseudo-terminal que nos va a permitir interaccionar con el contenedor.
    * `--rm`: si queremos que cuando finalice la ejecución del contenedor se borre.
    * `-d`: para que la ejecución de lo que le indiquemos en el contenedor se haga en segundo plano, de manera desatendida, sin estar conectada a la entrada y salida estándar.
    * `bash -c`: nos permite ejecutar uno o más comandos en el contenedor de forma más compleja.
    * `-e` o `--env`: para crear una variable de entorno al crear un contenedor.
    * `-p`: para mapear un puerto del Host Docker, con el puerto del servicio ofrecido por el contenedor ya que los contenedores que estamos creando se conectan a una red virtual privada y que toman direccionamiento dinámico. 

`docker ps`: lista los contenedores que se están ejecutando.
* Opciones:
    * `-a`: lista los contenedores que **NO** se están ejecutando.

`docker rm [CONTAINER_ID | NAME]`: elimina el conetenedor que indiquemos ya sea por su **id** o por su **name**.  
* Opciones:
    * `-f`: para forzar el borrado de un contenedor que está corriendo.

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
`docker attach`: nos conectamos a la entrada estándar y a la salida estándar y de error de un contenedor en ejecución, conectándonos a su terminal.    
`docker logs name_container`: para visualizar los logs del contenedor `name_container`.  
* Opciones:
    * `-f`: seguimos visualizando los logs en tiempo real.

`docker stop name_container`: para parar el contenedor `name_container`.  
`docker restart name_container`: reinicia la ejecución del contenedor `name_container`.  
`docker pause name_container`: pausa la ejecución del contenedor `name_container`.  
`docker unpause name_container`: continúa la ejecución del contenedor `name_container`.  
`docker exec name_container command`: para ejecutar comandos dentro de un contenedor.  
`docker cp origen destino`: para copiar ficheros a o desde un contenedor. Para indiar la parte del contenedor ya sea origen o destina lo indicaremos `name_container:[/ruta/]fichero`.  
`docker top name_container`: para visualizar los procesos que se están ejecutando en el contenedor `name_container`.  
`docker inspect name_container`: para obtener información de cualquier objeto Docker. Nos muestra mucha información en formato JSON por lo que es necesario filtrar lo que requiramos, por ejemplo:   
* El identificado del contenedor: `$ docker inspect --format='{{.Id}}' hora-container2`  
* El nombre de la imagen que hemos usado para crear el contenedor: `$ docker inspect --format='{{.Config.Image}}' hora-container2`  
* El valor de las variables de entorno definidas en el contenedor: `$ docker container inspect -f '{{range .Config.Env}}{{println .}}{{end}}' hora-container2`  
* El comando que hemos ejecutado en el contenedor: `$ docker inspect --format='{{range .Config.Cmd}}{{println .}}{{end}}' hora-container2`  
* La dirección IP que tiene el contenedor: `$ docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' hora-container2`
* Puertos que están mapeados de un contenedor: `$ docker inspect --format='{{range $p, $conf := .NetworkSettings.Ports}}  {{(index $conf 0).HostPort}} -> {{$p}} {{end}}' name_container`  

`docker port name_container`: ver los puertos que están mapeados en un contenedor.  
