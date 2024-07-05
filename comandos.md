`docker --version`: comprobar la versión.  
`docker version`: información de las versiones de los componentes.  
`docker info`: información del sistema que instalado.  
`docker run image`: crea y corre un contenedor basado en la imagen que indicamos en `image`.  
`docker ps`: lista los contenedores que se están ejecutando.
* Opciones:
    * `-a`: lista los contenedores que **NO** se están ejecutando.

`docker rm [CONTAINER_ID | NAME]`: elimina el conetenedor que indiquemos ya sea por su **id** o por su **name**.  
`docker create image`: **SOLO** crea un contenedor basado en la imagen `image` pero **NO** lo inicia.  
`docker start name_container`: inicia la ejecución del contenedor `name_container`.  
* Opciones:
    * `-a`: nos permite conectar a la salida estándar del contenedor y poder ver en nuestro terminal la salida.
