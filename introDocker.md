# INTRODUCCIÓN A DOCKER

## Introducción a Docker.

### Introducción a los contenedores  

La virtualización utiliza el software para imitar las caracterísitcas del hardwaer y crear un sistema informático virtual.  

**¿Por qué se utiliza?**
* Aislamiento e independencia de servicios y contenidos.
* Laboratorio de pruebas.
* Virtualización de arquitecturas de las que no se dispone.
* Creación de clúster de máquinas y sistemas distribuidos.
* Herramienta de aprendizajes

**Ventajas**
* Importante ahorro económico.
* Seguridad.
* Mayor aprovechamiento de recursos.
* Migración en vivo.
* Importante ahorro energético.

**Inconvenientes**
* Muchos sistemas dependen de un solo equipo físico.
* Penalizaciones en rendimiento.

**Tipos de virtualización**  
* *Emulación*: El sistema de virtualización imita o suplanta vía software una arquitectura al completo (procesador, memoria, conjunto de instrucciones, comunicaciones...). Ejemplo: QEMU, Microsoft Virtual PC, Wine, ...
* *Virtualización por hardware de tipo 1*: Simula un hardware suficiente para permitir que un sistema operativo no adaptado se ejecute de forma aislada. Controla directamente el hardware físico del host ofreciéndolo directamente a la máquina virtual. Ejemplos: Xen, Kernel-based Virtual Machine (KVM), Microsoft Hyper-V, VMware ESXi,...
* *Virtualización completa de tipo 2*: En este caso este software no controla directamente el hardware físico, por lo que el rendimiento puede ser menor que el anterior. Ejemplos: VMware Workstation, Parallels Desktop, VirtualBox, VMware Player, ...
* *Virtualización ligera*: O también llamada virtualización a nivel de sistema operativo, o virtualización basada en contenedores. Es un método de virtualización en el que, sobre el núcleo del sistema operativo se ejecuta una capa de virtualización que permite que existan múltiples instancias aisladas de espacios de usuario. A cada espacio de usuario aislado lo llamamos contenedor.

**Contenedores**  
Un contenedor es un conjunto de procesos aislados, que se ejecutan en un servidor, y que acceden a un sistema de ficheros propio, tienen una configuración de red propia y acceden a los recursos del host (memoria y CPU). Utilizan para su funcionamiento el núcleo del host donde se ejecutan.  
Podemos hacer la siguiente clasificación de contenedores dependiendo de su uso:  
* *Contenedores de Sistemas*: El uso que se hace de ellos es muy similar al que hacemos sobre una máquina virtual: se accede a ellos (normalmente por ssh), se instalan servicios, se actualizan, ejecutan un conjunto de procesos... Ejemplo: LXC(Linux Container).
* *Contenedores de Aplicación*: Se suelen usar para el despliegue de aplicaciones web. Ejemplo: Docker, Podman...

**Contenedores y aplicaciones**  
¿Qué aplicaciones web son más idóneas para desplegar en contenedores?  
* Si tenemos *aplicaciones monolíticas*, vamos a usar un esquema multicapa, es decir cada servicio (servicio web, servicio de base de datos... ) se va a desplegar en un contenedor.  
* Realmente, las aplicaciones que mejor se ajustan al despliegue en contenedores son la desarrolladas con *microservicios*:
    * Cada componente de la aplicación (“microservicio”) se puede desplegar en un contenedor.
    * Comunicación vía HTTP API REST y colas de mensajes.
    * Facilita enormemente las actualizaciones de versiones de cada componente.

**Ventajas del uso de contenedores de aplicaciones**
* *Portabilidad*: Los contenedores encapsulan una aplicación y todas sus dependencias de manera aislada. Esto facilita la portabilidad, ya que los contenedores pueden ejecutarse de manera consistente en diferentes entornos, como desarrollo, pruebas y producción.
* *Aislamiento*: Los contenedores proporcionan un nivel de aislamiento entre la aplicación y el sistema operativo del anfitrión. Esto asegura que las aplicaciones se ejecuten sin interferencias con otras aplicaciones o componentes del sistema, evitando conflictos de dependencias y problemas de compatibilidad.
* *Eficiencia en el uso de recursos*: Al compartir el núcleo del sistema operativo y solo incluir las bibliotecas y dependencias necesarias, los contenedores son más eficientes en términos de recursos en comparación con las máquinas virtuales. Esto permite una utilización más efectiva de los recursos del sistema y una mayor densidad de aplicaciones por servidor.
* *Despliegue rápido*: Los contenedores permiten la creación, el despliegue y la escalabilidad rápida de aplicaciones. La capacidad de implementar contenedores en cuestión de segundos o minutos facilita la entrega continua y el despliegue ágil de aplicaciones.  

### Introducción a Docker

#### Docker

* Docker es una tecnología de virtualización "ligera" cuyo elemento básico es la utilización de contenedores en vez de máquinas virtuales y cuyo objetivo principal es el despliegue de aplicaciones encapsuladas en dichos contenedores.
* Docker es una plataforma de código abierto diseñada para facilitar la creación, implementación y ejecución de aplicaciones en entornos contenerizados.
* "Docker": estibador.
* Pertenece a los denominados contenedores de aplicaciones
* Nuevo paradigma. Cambia completamente la forma de desplegar y distribuir una aplicación basado en el lema build, ship and run. (Construye, distribuye y ejecuta).
* Lo desarrolla la empresa Docker, Inc, pero actualmente es un proyecto perteneciente a la Cloud Native Computing Foundation (CNCF) con lo que se asegura el desarrollo de los estándares que se utilizan.
* Software libre.

#### Objetos Docker

* **Contenedor**:
    * Entorno aislado donde se ejecuta una aplicación.
    * Tiene su propio sistema de ficheros con todas las dependencias que necesita la aplicación para funcionar.
    * Puede estar conectado a una red virtual y utilizar almacenamiento adicional para no perder la información importante.
    * Utiliza los recursos del servidor donde se está ejecutando (núcleo del sistema operativo, CPU, RAM).
    * Los contenedores Docker suelen ejecutar un sólo proceso.
    * Los contenedores Docker son efímeros
* **Imagen**:
    * Una imagen es una plantilla de sólo lectura con instrucciones para crear un contenedor Docker.
    * Contiene el sistema de fichero que tendrá el contenedor.
    * Además establece el comando que ejecutará el contenedor por defecto.
    * Podemos crear nuestras propias imágenes o utilizar las creadas por otros y publicadas en un registro.
    * Un contenedor es una instancia ejecutable de una imagen.
* **Redes**, **Volúmenes**, **Plugins**...

#### Arquitectura de Docker
Docker utiliza una arquitectura cliente-servidor. El cliente Docker se comunica (usando una API REST) con el demonio Docker, encargado de gestionar las imágenes, contenedores, volúmenes, redes...
<img width="616" alt="arquitecturadocker" src="https://github.com/eguirod/docker/assets/71733548/6848e9de-c481-4304-9f2d-855787542b26">
* El **demonio Docker** (**Docker Engine**): Ofrece una API REST que utiliza el cliente Docker, y gestiona los objetos Docker.
    * El ordenador donde está instalado el demonio Docker lo llamaremos *Host Docker*.
    * De forma predeterminada el demonio Docker y los contenedores que gestionan se ejecutan por el usuario administrador del sistema.
    * Podemos instalador Docker para ser usado por usuario sin privilegios (modo rootless), aunque tiene algunas limitaciones se consigue tener más seguridad.
* El **cliente Docker**: Usando el comando `docker` nos comunicamos con el demonio Docker para gestionar los objetos Docker con los que trabajamos. El cliente y el demonio pueden estar en equipos distintos.
* **Registros Docker**: Un registro Docker almacena imágenes Docker. *Docker Hub* es un registro público que cualquiera puede utilizar, y Docker busca imágenes en Docker Hub de forma predeterminada. Podemos instalar en nuestros servidores registros privados.
* **Docker Desktop**: Aplicación gráfica que permite la gestión sencilla de objetos Docker. Incluye el demonio y el cliente Docker.
* **Docker Swarm**: Es la solución de orquestación de contenedores ofrecida por Docker.

#### Docker en la actualidad

Podemos obtener Docker de varias formas:
* **Moby**: Proyecto de comunidad (docker.io de debian/ubuntu). [Más información](https://mobyproject.org/).
* **Docker CE**: Componentes de Docker proporcionado por la empresa Docker inc.
    * Para uso *personal* es gratuito.
    * Para uso *profesional*, ofrecen distintos tipos de suscripciones con diferentes precios:
        * Pro, Team, Business. [Más información](https://www.docker.com/pricing/).  

#### Instalar Docker CE

Dos opciones:
* Instalar **Docker Engine**:
    * Incluye el cliente y el demonio Docker.
    * Sólo se puede instalar en distribuciones Linux: CentOS, Debian, Fedora, Ubuntu...
* Instalar **Docker Desktop**:
    * Incluye el cliente y el demonio Docker.
    * El demonio Docker se ejecuta en una máquina virtual.
    * Nos ofrece una aplicación gráfica para gestionar los objetos Docker.
    * Es necesario tener entorno gráfico.
    * Incluye algunas otras funcionalidades...
    * Se puede instalar en Linux, Windows y Mac.

#### Alternativas a Docker

Otras empresas han desarrollado software de contenedores de aplicación:
* **podman**: Creado por Red Hat como alternativa a Docker. [Más información](https://podman.io/).
* **containerd**: Inicialmente desarrollado por Docker, containerd es un componente fundamental en la arquitectura de Docker que ha sido separado como un proyecto independiente y es parte de la Cloud Native Computing Foundation (CNCF). [Más información](https://containerd.io/).
* **CRI-O**: También desarrollado por Red Hat y parte de la CNCF, CRI-O se centra en proporcionar una implementación liviana y especializada para la ejecución de contenedores en entornos de Kubernetes. [Más información](https://cri-o.io/).
* **pouch**: Otro sistema de contenedores creado por la empresa Alibaba como alternativa a Docker. [Más información](https://pouchcontainer.io/#/).

#### Limitaciones de Docker

* El proceso de actualización de versiones en producción.
* ¿Cómo se balancea la carga entre contenedores iguales?
* ¿Cómo se conectan contenedores que se ejecutan en diferentes demonios de Docker?
* ¿Se puede hacer una actualización de una aplicación sin interrupción?
* ¿Se puede variar a demanda el número de réplicas de un determinado contenedor?
Las respuestas a estas preguntas y otras similares tiene que venir del uso de un Orquestador de Contenedores.

Un **Orquestador de contenedores** es un programa que gestiona los contenedores que se ejecutan en un clúster de servidores. Nos ofrece muchas características: Actualizaciones automáticas, balanceo de carga, tolerancia a fallos, escalabilidad...  
Distintas alternativas:
* Docker Swarm
* Apache Mesos
* Hashicorp Nomad
* Kubernetes

Hoy en día se acepta generalmente que el vencedor ha sido kubernetes. ¿Por qué?: Gran cantidad de empresas implicadas en su desarrollo, iniciada por Google pero donada a la CNCF con una versión inicial muy madura, gran número de aplicaciones complementarias,. . .
El resto de proyectos siguen activos, como alternativas más sencillas a k8s o en su propio nicho.

### Instalación de Docker Engine en Linux

Docker Engine está disponible en varias distribuciones de Linux, macOS y Windows a través de Docker Desktop y como instalación binaria estática, sólo se puede instalar en distribuciones Linux.  
En este apartado vamos a realizar la instalación binaria de Docker Engine sobre una distribución Linux Ubuntu 22.04. Puedes seguir la [documentación oficial](https://docs.docker.com/engine/install/) para aprender el método de instalación en otros sistemas.  
Para el sistema operativo Ubuntu puedes seguir las instrucciones y requerimientos en el siguiente [enlace](https://docs.docker.com/engine/install/ubuntu/). Suponemos que vamos a realizar la instalación en un sistema operativo que no tiene instalado versiones antiguas de Docker.  
Tenemos varios métodos de instalación disponible: instalando Docker Desktop, usando los repositorios oficiales de Docker, descargando manualmente los ficheros deb o ejecutando un script de instalación.  
En nuestro caso usaremos los repositorios apt de de Docker, para ello:
1. Actualizamos los repositorios e instalamos los paquetes necesarios para instalar desde repositorios HTTPS:
```
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
```
2. Añadir la clave GPG oficial de Docker:
```
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
3. Añadimos el repositorio oficial de Docker:
```
echo \
"deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
"$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
4. Instalamos Docker Engine:
```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Para manejar Docker con un usuario sin privilegio, debemos añadir el usuario al grupo `docker`, para ello: `sudo usermod -aG docker $USER`.  
Debes volver a iniciar una terminal con el usuario, o ejecutar el siguiente comando: `su - $USER`.  
Y finalmente, comprobamos la versión con la que vamos a trabajar: `docker --version`.  
Si queremos más información de las versiones de los componentes con los que vamos a trabajar, ejecutamos: `docker version`.   
Para más información del sistema que hemos instalado podemos ejecutar: `docker info`.  

### Instalación de Docker Desktop en Linux

Podemos instalar Docker Desktop en distintas distribuciones Linux: Debian, Fedora, Ubuntu,... En este apartado vamos a realizar la instalación en la distribución Ubuntu.  
Los requisitos mínimos necesarios son:
* CPU con arquitectura de 64 bits y soporte de virtualización.
* Virtualización KVM.
* Entorno gráfico Gnome, KDE o MATE.
* 4 Gb de RAM.
* A partir de Ubuntu 22.04.  

Pasos a seguir:
1. Configuramos los repositorios de Docker:
```
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
"deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
"$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
2. Descargamos el paquete deb de la página oficial de instalación.
3. Instalamos Docker Desktop:
```
sudo apt-get update
sudo apt-get install ./docker-desktop-<version>-<arch>.deb
```
La `<version>` y el `<arch>` dependerán de qué versión y arquitectura te hayas descargado.
4. Tendremos a nuestra disposición un icono que permite iniciar Docker Desktop. En este momento se iniciará la máquina virtual donde se está ejecutando el demonio Docker. También tenemos a nuestra disposición en la máquina donde hemos instalado Docker Desktop el cliente Docker:
```
$ docker version
Client: Docker Engine - Community
 Cloud integration: v1.0.35+desktop.10
 Version:           25.0.3
 ...
Server: Docker Desktop 4.27.2 (137060)
 Engine:
  Version:          25.0.3
  ...
```  

#### Autentificación en Docker Hub desde Docker Desktop  

**Docker Hub** es el registro público de imágenes Docker. De este registro vamos a descargar las imágenes que necesitemos. Si queremos subir al registro nuestras propias imágenes tendremos que registrarnos en este servicio.  
Desde **Docker Desktop** podemos autentificarnos en Docker Hub con nuestra cuenta, de esta manera podremos gestionar nuestras imágenes en el registro.  
En distribuciones Linux vamos a usas claves GPG para cifrar las credenciales de acceso, y estas credenciales se van almacenar usando la utilidad pass.  
Lo primero que tenemos que hacer es inicializar un par de claves GPG (pública y privada), para ello:
```
$ gpg --generate-key
...
gpg: clave 09FFD80DB166C498 marcada como de confianza absoluta
gpg: creado el directorio '/home/usuario/.gnupg/openpgp-revocs.d'
gpg: certificado de revocación guardado como '/home/usuario/.gnupg/openpgp-revocs.d/B4901885C051839E8CBEA0E609FFD80DB166C498.rev'
claves pública y secreta creadas y firmadas.

pub   rsa3072 2024-02-15 [SC] [caduca: 2026-02-14]
      B4901885C051839E8CBEA0E609FFD80DB166C498
uid                      José Domingo Muñoz <josedom24@example.com>
sub   rsa3072 2024-02-15 [E] [caduca: 2026-02-14]
```
Durante la generación nos pedirá nuestro nombre y apellidos, nuestro correo electrónico y nos pedirá una "frase de paso" para asegurar el uso de la clave privada que estamos creando.  
A continuación inicializaremos la utilidad pass usando la clave pública que hemos creado, tenemos que indicar el campo ID de la clave pública:
```
$ pass init B4901885C051839E8CBEA0E609FFD80DB166C498
mkdir: se ha creado el directorio '/home/usuario/.password-store/'
Password store initialized for B4901885C051839E8CBEA0E609FFD80DB166C498
```  
En el directorio `/home/usuario/.password-store/` se guardarán las credenciales cifradas de acceso a Docker Hub.  
Para finalizar, desde Docker Desktop podemos pulsar sobre el botón Sign In para loguearnos en Docker Hub. Y podremos comprobar que estamos autentificados de forma correcta.

### Instalación de Docker Desktop en Windows  

Podemos instalar Docker Desktop en distintas versiones del sistema operativo Windows: En este apartado vamos a realizar la instalación en windows 10 Pro (versión 22H2). En sistemas Windows Docker Desktop instala el demonio Docker o sobre una máquina Linux usando WSL (Subsistema de Windows para Linux) o usando una máquina virtual ejecutada sobre el hipervisor Hyper-V. Nosotros vamos a usar la primera opción de instalación.  
Los requisitos mínimos necesarios son:  
* CPU con arquitectura de 64 bits y soporte de virtualización en BIOS.
* WSL versión 1.1.3.0 o superior, con posibilidad de pasar a WSL 2.
* Windows 11 64-bit: Home, Pro. Enterprise o Education (versión 21H2 o superior).
* Windows 10 64-bit: Recomendado Home, Pro. Enterprise o Education (versión 22H2 build 19045 o superior), aunque se puede usar Home, Pro. Enterprise o Education (versión 21H2 build 19044 o superior).
* 4 Gb de RAM.  

Pasos a seguir:
1. Descargamos el instalador mediante el botón de descarga de la página de instalación.
2. Ejecutamos el instalador haciendo doble click en `Docker Desktop Installer.exe`. De forma predeterminada, Docker Desktop se instala en `C:\Archivos de programa\Docker\Docker`.
3. Durante la instalación elegiremos la opción Utilizar WSL 2 en lugar de Hyper-V. Si su sistema sólo admite una de las dos opciones, no podrá seleccionar qué backend utilizar.
4. Siga las instrucciones del asistente de instalación para autorizar al instalador y proceder con la instalación.
5. Cuando la instalación se haya realizado correctamente, seleccione Close & restart para completar el proceso de instalación.
6. Después del reinicio tendremos un icono para ejecutar Docker Desktop, y si queremos pulsando sobre el botón Sign in nos podremos autentificar con nuestra cuenta de Docker Hub.  
Por último, si accedemos a una terminal ejecutando PowerShell o cmd, podemos usar el cliente Docker.

## Ejecución de contenedores.

### El "Hola Mundo" de Docker  

Vamos a crear nuestro primer contenedor, para comprobar que todo está funcionando y vamos a explicar el proceso que se va a realizar en la creación del contenedor.  
```
$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
719385e32844: Pull complete 
Digest: sha256:a13ec89cdf897b3e551bd9f89d499db6ff3a7f44c5b9eb8bca40da20eb4ea1fa
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

Pero, ¿qué es lo que está sucediendo al ejecutar esa orden?:

1. El cliente Docker se conecta al demonio Docker y le indica que debe crear un contenedor (docker run).
2. Al ser la primera vez que se ejecuta un contenedor basado en la imagen hello-word, la imagen se descarga del registro público llamado Docker Hub y se guarda en nuestro registro local.
3. Se crea el contenedor que ejecuta un comando que muestra el mensaje que hemos leído.
4. El mensaje se envía al cliente Docker que nos lo muestra en el terminal.

NOTA: En realidad todas los comandos del cliente Docker que trabajan con contenedores son subcomandos de docker container, pero se puede abreviar omitiendo el comando container, es decir estos dos comandos son iguales:
```
$ docker container run ...
$ docker run...
```

Si listamos los contenedores que se están ejecutando (`docker ps`):
```
$ docker ps
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS    PORTS     NAMES
```

Comprobamos que este contenedor no se está ejecutando. Un contenedor ejecuta un proceso y cuando termina la ejecución, el contenedor se para.  

Para ver los contenedores que no se están ejecutando (observa que se ha asignado un nombre aleatorio al contenedor), ejecutamos:
```
$ docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                    PORTS     NAMES
e5ea0c675f71   hello-world   "/hello"   31 seconds ago   Exited (0) 29 seconds ago           quirky_hellman
```

Como podemos observar el script que ha ejecutado el contenedor se llama /hello.  

Para eliminar el contenedor podemos identificarlo con su id:
`$ docker rm e5ea0c675f71`  

o con su nombre:
`$ docker rm quirky_hellman`  

#### Creación de contenedores sin ejecutarlos  

De manera habitual vamos a usar docker run para crear y ejecutar un contenedor. Podríamos también crear un contenedor que no se ejecute y posteriormente dar la orden de ejecución. Vamos a observar que la creación de este segundo contenedor será mucho más rápida ya que tenemos la imagen descargada en nuestro registro local. Para crear un contenedor y no iniciar su ejecución utilizaremos el comando docker create:
`$ docker create hello-world`  

Podemos ver que el contenedor está creado pero no en ejecución:
```
$ docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS    PORTS     NAMES
590ac3f01de5   hello-world   "/hello"   6 seconds ago   Created             focused_morse
```

Podemos iniciar la ejecución de este contenedor usando `docker start -a`. La opción `-a` nos permite conectar a la salida estándar del contenedor y poder ver en nuestro terminal la salida.
```
$ docker start -a focused_morse

Hello from Docker!
...
```

### Ejecución simple de contenedores  

En este apartado vamos a crear un contenedor especificando el comando que debe ejecutar a partir de la imagen ubuntu. En este caso vamos a descargar primero la imagen del registro público Docker Hub, y a continuación crearemos el contenedor.  
Para descargar una imagen de Docker Hub, ejecutamos el comando docker pull:  
```
$ docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
29202e855b20: Pull complete 
Digest: sha256:e6173d4dc55e76b87c4af8db8821b1feae4146dd47341e4d431118c7dd060a74
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
```
Los nombres de las imágenes tienen 2 partes, el nombre y una etiqueta. Sino indicamos la etiqueta la utilizada será la latest, que indica que se está bajando la última versión.
A continuación, creamos y ejecutamos un nuevo contenedor indicando el comando que va a ejecutar:  
```
$ docker run ubuntu echo 'Hello world'
Hello world
```  
Comprobamos que el contenedor ha ejecutado el comando que hemos indicado y se ha parado:  
```
$ docker ps -a
CONTAINER ID        IMAGE              COMMAND                  CREATED               STATUS                      PORTS               NAMES
3bbf39d0ec26        ubuntu             "echo 'Hello wo…"        31 seconds ago        Exited (0) 29 seconds ago                       wizardly_edison
```  
Los contenedores que hemos creado se nombran de manera aleatoria. Podemos cambiar el nombre de cualquier contenedor usando el comando docker rename:  
```
$ docker rename wizardly_edison contenedor_ubuntu
```  
Y comprobamos que el nombre ha cambiado:  
```
$ docker ps -a
CONTAINER ID   IMAGE     COMMAND                CREATED         STATUS                     PORTS     NAMES
5bd9366588ef   ubuntu    "echo 'Hello world'"   6 minutes ago   Exited (0) 5 minutes ago             contenedor_ubuntu
```

#### Visualizando las imágenes de nuestro registro local  

Con el comando docker images (también se puede usar docker image ls, docker image list) podemos visualizar las imágenes que ya tenemos descargadas en nuestro registro local:  
```
$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
ubuntu        latest    e34e831650c1   11 days ago    77.9MB
hello-world   latest    d2c94e258dcb   8 months ago   13.3kB
```

#### ¿Qué ocurre cuando creamos un contenedor?  

Para terminar podemos ver las distintas etapas por las que pasa la creación de un contenedor ejecutando docker events. Para ello en una terminal ejecutamos el comando:  
```
$ docker events
```  
Y en otro terminal ejecutamos un contenedor:  
```
$ docker run ubuntu echo 'Hello world'
```

En el primer terminal veremos las operaciones que se han dio produciendo:  
```
2024-01-22T21:08:37.947946863+01:00 container create 6167a0dbc036143fcd9d3b2783f6d507fbd72900622f8929a5424dee9264e9f5 (image=ubuntu, name=loving_jennings, org.opencontainers.image.ref.name=ubuntu, org.opencontainers.image.version=22.04)
2024-01-22T21:08:37.953203114+01:00 container attach 6167a0dbc036143fcd9d3b2783f6d507fbd72900622f8929a5424dee9264e9f5 (image=ubuntu, name=loving_jennings, org.opencontainers.image.ref.name=ubuntu, org.opencontainers.image.version=22.04)
2024-01-22T21:08:38.310303971+01:00 network connect 7e6404027e1ec38230c4dc35f40079c6f6366cd61d73a472517e39f598cebab1 (container=6167a0dbc036143fcd9d3b2783f6d507fbd72900622f8929a5424dee9264e9f5, name=bridge, type=bridge)
2024-01-22T21:08:38.966836361+01:00 container start 6167a0dbc036143fcd9d3b2783f6d507fbd72900622f8929a5424dee9264e9f5 (image=ubuntu, name=loving_jennings, org.opencontainers.image.ref.name=ubuntu, org.opencontainers.image.version=22.04)
2024-01-22T21:08:39.392255443+01:00 network disconnect 7e6404027e1ec38230c4dc35f40079c6f6366cd61d73a472517e39f598cebab1 (container=6167a0dbc036143fcd9d3b2783f6d507fbd72900622f8929a5424dee9264e9f5, name=bridge, type=bridge)
2024-01-22T21:08:40.227050098+01:00 container die 6167a0dbc036143fcd9d3b2783f6d507fbd72900622f8929a5424dee9264e9f5 (execDuration=0, exitCode=0, image=ubuntu, name=loving_jennings, org.opencontainers.image.ref.name=ubuntu, org.opencontainers.image.version=22.04)
```

### Más opciones en la ejecución de contenedores  

Hemos usado el comando docker run para crear y ejecutar contenedores. Este comando tiene muchas opciones, veamos algunas de ellas:  

#### Nombrar los contenedores  

A la hora de la creación del contenedor podemos ponerle un nombre (usando el parámetro --name) y también, podemos indicar el hostname (con al opción -h o --hostname). Veamos un ejemplo:  
```
$ docker run --name contenedor1 -h contendor_ubuntu ubuntu hostname
contendor_ubuntu
```  
Hemos comprobado que el hostname lo hemos configurado, y veamos que el nombre del contenedor también lo hemos configurado:  
```
$ docker ps -a
CONTAINER ID   IMAGE     COMMAND      CREATED          STATUS                      PORTS     NAMES
cea2a22ac6aa   ubuntu    "hostname"   56 seconds ago   Exited (0) 54 seconds ago             contenedor1
```  

#### Ejecutando un contenedor interactivo  

En este caso usamos la opción -i para abrir una sesión interactiva, -t nos permite crear un pseudo-terminal que nos va a permitir interaccionar con el contenedor. El comando que vamos a ejecutar en el contenedor es bash para que podamos acceder al terminal:  
```
$ docker run -it --name contenedor2 -h cont2 ubuntu bash 
root@cont2:/#
```  
El contenedor se para cuando salimos de él. Para volver a conectarnos a él:  
```
$ docker start contenedor2
contendor2
$ docker attach contenedor2
root@cont1:/#
```  
Con docker attach nos conectamos a la entrada estándar y a la salida estándar y de error de un contenedor en ejecución, conectándonos a su terminal.  
En realidad, todas las imágenes tienen definidas un proceso que se ejecuta por defecto si no se indica de manera explicita cuando creamos el contenedor. En concreto, la imagen ubuntu (y en general todas las imágenes que corresponden al sistemas operativos) tiene definida por defecto el proceso bash, por lo que podríamos haber ejecutado:  
```
$ docker run -it --name contenedor2 ubuntu
```  

#### Eliminación automática de un contenedor  

Como hemos visto hasta ahora cuando un contenedor termina de ejecutar el comando indicado, se para. Si queremos que cuando finalice la ejecución del contenedor se borre, usaremos la opción --rm. Por ejemplo:  
```
docker run -it --rm --name contenedor3 ubuntu top
```  
Cuando salgamos de ejecutar el comando top se borrará el contenedor. Puedes ejecutar un docker ps -a para comprobarlo.  

#### Ejecutando un contenedor demonio  

En esta ocasión hemos utilizado la opción -d del comando docker run, para que la ejecución del comando en el contenedor se haga en segundo plano, de manera desatendida, sin estar conectada a la entrada y salida estándar.  
```
$ docker run -d --name contenedor4 ubuntu bash -c "while true; do echo hello world; sleep 1; done"
7b6c3b1c0d650445b35a1107ac54610b65a03eda7e4b730ae33bf240982bba08
```  
NOTA: En la instrucción docker run hemos ejecutado el comando con bash -c que nos permite ejecutar uno o más comandos en el contenedor de forma más compleja (por ejemplo, indicando ficheros dentro del contenedor).  
Comprobamos que el contenedor se está ejecutando:  
```
$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
c6b1761c8831   ubuntu    "bash -c 'while true…"   5 seconds ago   Up 2 seconds             contenedor4
```  
Podemos visualizar los logs del contenedor, ejecutando el siguiente comando:  
```
$ docker logs contenedor4
```  
Con la opción logs -f seguimos visualizando los logs en tiempo real.  
Por último podemos parar el contenedor y borrarlo con las siguientes instrucciones:  
```
$ docker stop contenedor4
$ docker rm contenedor4
```  
Hay que tener en cuenta que un contenedor que esta ejecutándose no puede ser eliminado. Tendríamos que parar el contenedor y posteriormente borrarlo. Otra opción es borrarlo a la fuerza:  
```
$ docker rm -f contenedor4
```

#### Configuración de contenedores con variables de entorno  

Más adelante veremos que al crear un contenedor que necesita alguna configuración específica, lo que vamos a hacer es crear variables de entorno en el contenedor, para que el proceso que inicializa el contenedor pueda realizar dicha configuración.  
Para crear una variable de entorno al crear un contenedor usamos el flag -e o --env:  
```
$ docker run -it --name contenedor5 -e USUARIO=prueba ubuntu bash
root@91e81200c633:/# echo $USUARIO
prueba
```

### Gestión de contenedores Docker  

#### Ciclo de vida de los contenedores  

Para ver un ejemplo de los comandos que gestionan el ciclo de vida de un contenedor vamos a ejecutar un contenedor demonio que va escribiendo la hora cada segundo, para ver la salida visualizamos sus logs:
```
$ docker run -d --name hora-container ubuntu bash -c 'while true; do echo $(date +"%T"); sleep 1; done'
$ docker logs -f hora-container
```

En otra terminal vamos ejecutando los comandos que nos permiten controlar su ciclo de vida:  
`docker start`: Inicia la ejecución de un contenedor que está parado.  
`docker stop`: Detiene la ejecución de un contenedor en ejecución.  
`docker restart`: Para y vuelve a iniciar la ejecución de un contenedor.  
`docker pause`: Pausa la ejecución de un contenedor.  
`docker unpause`: Continúa la ejecución de un contenedor que estaba pausado.  

#### Ejecución de comandos en contenedores  

Si tenemos un contenedor que está iniciado, podemos ejecutar comandos en él con `docker exec`. En esta ocasión vamos a crear un contenedor que hace algo parecido al anterior, pero en este caso guarda la hora en un fichero cada segundo:  
```
$ docker run -d --name hora-container2 ubuntu bash -c 'while true; do date +"%T" >> hora.txt; sleep 1; done'
$ docker exec hora-container2 ls
...
hora.txt
...
$  docker exec hora-container2 cat hora.txt
```

#### Copiar ficheros en contenedores  

Con el comando docker cp podemos copiar ficheros a o desde un contenedor. Por ejemplo, si tengo un fichero en mi equipo lo puedo copiar al contenedor:
```
$ echo "Curso Docker">docker.txt
$ docker cp docker.txt hora-container2:/tmp
Successfully copied 2.05kB to hora-container2:/tmp
```

Podemos comprobar que el fichero existe en el contenedor:
```
$ docker exec hora-container2 cat /tmp/docker.txt
Curso Docker
```

Evidentemente, también podemos copiar ficheros desde el contenedor a nuestro equipo:
```
docker cp hora-container2:hora.txt .
Successfully copied 5.63kB to /home/usuario/.
```

#### Visualizar procesos que se ejecutan en un contenedor  

Podemos visualizar los procesos que se están ejecutando en un contenedor con el comando docker top:
```
$ docker top hora-container2
```  

#### Obtener información de los contenedores  

Para obtener información de cualquier objeto Docker vamos a usar el subcomando inspect. En el caso de los contenedores, ejecutamos:
```
$ docker inspect hora-container2
```

Nos muestra mucha información en formato JSON (JavaScript Object Notation) y nos da datos sobre aspectos como:
* El id del contenedor.
* Los puertos abiertos y sus redirecciones.
* Los bind mounts y volúmenes usados.
* El tamaño del contenedor (si ejecutamos docker inspect -s).
* La configuración de red del contenedor.
* El comando que se esta ejecutando en el contenedor.
* El valor de las variables de entorno.
* Y muchas más cosas...  

Como nos devuelve mucha información podemos filtrar los campos que nos interesan, por ejemplo:  
El identificado del contenedor: `$ docker inspect --format='{{.Id}}' hora-container2`  
El nombre de la imagen que hemos usado para crear el contenedor: `$ docker inspect --format='{{.Config.Image}}' hora-container2`  
El valor de las variables de entorno definidas en el contenedor: `$ docker container inspect -f '{{range .Config.Env}}{{println .}}{{end}}' hora-container2`  
El comando que hemos ejecutado en el contenedor: `$ docker inspect --format='{{range .Config.Cmd}}{{println .}}{{end}}' hora-container2`  
La dirección IP que tiene el contenedor: `$ docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' hora-container2`  

### Ejemplo: Creando un contenedor con un servidor web  

En este ejemplo vamos a crear un contenedor demonio que ejecuta un servidor web Apache, para ello vamos a usar la imagen httpd:2.4 del registro Docker Hub (en este caso hemos indicado el nombre de la imagen y su etiqueta 2.4 que nos indica la versión del servidor web que vamos a usar):
```
$ docker run -d --name my-apache-app -p 8080:80 httpd:2.4
```  

Hay que tener en cuenta que los contenedores que estamos creando se conectan a una red virtual privada y que toman direccionamiento dinámico. No solemos usar la dirección IP del contenedor para acceder al servicio que nos ofrece. Con la opción `-p` mapeamos un puerto del Host Docker, con el puerto del servicio ofrecido por el contenedor. Si accedemos a la dirección IP del ordenador que tiene instalado Docker al primer puerto indicado, se redireccionará la petición a la dirección IP del contenedor al segundo puerto indicado. Nunca utilizamos directamente la dirección IP del contenedor para acceder a él.  

Podemos ver los puertos que están mapeados en un contenedor de dos maneras distintas. Usando el comando docker port:
```
$ docker port my-apache-app
80/tcp -> 0.0.0.0:8080
80/tcp -> [::]:8080
```  
O utilizando el comando docker inspect con un filtro:
```
$ docker inspect --format='{{range $p, $conf := .NetworkSettings.Ports}}  {{(index $conf 0).HostPort}} -> {{$p}} {{end}}' my-apache-app
```  
Para probarlo accedemos desde un navegador web.  
* Si estamos accediendo desde el Host Docker, accederemos a http://localhost:8080.  
* Si estamos accediendo desde un ordenador remoto, accederemos a la dirección IP del Host Docker y al puerto, por ejemplo,si dirección IP del Host Docker es 192.168.121.54, accederemos a http://192.168.121.54:8080:

Para acceder al log del contenedor podemos ejecutar:
```
$ docker logs my-apache-app
```

#### Modificación del contenido servido por el servidor web  

Si consultamos la documentación de la imagen httpd en el registro Docker Hub, podemos determinar que el servidor web que se ejecuta en el contenedor guarda los ficheros que sirve (directorio DocumentRoot) en `/usr/local/apache2/htdocs/`. Vamos a crear un nuevo fichero index.html en ese directorio.  
Lo podemos hacer de varias formas:
* Accediendo de forma interactiva al contenedor y haciendo la modificación:
```
$ docker exec -it my-apache-app bash
root@cf3cd01a4993:/usr/local/apache2# cd /usr/local/apache2/htdocs/
root@cf3cd01a4993:/usr/local/apache2/htdocs# echo "<h1>Curso Docker</h1>" > index.html
root@cf3cd01a4993:/usr/local/apache2/htdocs# exit
```  
* Ejecutando directamente el comando de creación del fichero index.html en el contenedor:
```
$ docker exec my-apache-app bash -c 'echo "<h1>Curso Docker</h1>" > /usr/local/apache2/htdocs/index.html'
```  
* Usando el comando docker cp y copiando el fichero index.html al contenedor:
``` 
$ echo "<h1>Curso Docker</h1>" > index.html
$ docker cp index.html  my-apache-app:/usr/local/apache2/htdocs/
```  
Independientemente de cómo hayamos creado el fichero, podemos volver a acceder al servidor web y comprobar que efectivamente hemos cambiado el contenido del index.html.  

### Ejemplo: Configuración de un contenedor con la imagen MariaDB  

En ocasiones es obligatorio el inicializar alguna variable de entorno para que el contenedor pueda ser ejecutado. Si miramos la documentación en Docker Hub de la imagen mariadb, observamos que podemos definir algunas variables de entorno para la creación y configuración del contenedor (por ejemplo: MARIADB_DATABASE,MARIADB_USER, MARIADB_PASSWORD,...). Pero hay una que la tenemos que indicar de forma obligatoria, la contraseña del usuario root (MARIADB_ROOT_PASSWORD), por lo tanto:
```  
$ docker run -d --name mimariadb -e MARIADB_ROOT_PASSWORD=my-secret-pw mariadb:10.5
$ $ docker ps
CONTAINER ID   IMAGE       COMMAND                  CREATED          STATUS         PORTS             NAMES
09425481aee6   mariadb     "docker-entrypoint.s…"   22 seconds ago   Up 1 second    3306/tcp          mimariadb
```

Podemos ver que se ha creado una variable de entorno:
```  
$ docker exec -it mimariadb env
...
MARIADB_ROOT_PASSWORD=my-secret-pw
...
```

Y para acceder podemos ejecutar:
```
$ docker exec -it mimariadb bash
root@9c3effd891e3:/# mysql -u root -p"$MARIADB_ROOT_PASSWORD" 
...

MariaDB [(none)]>
```  

Otra forma de hacerlo sería:
```
$ docker exec -it mimariadb mysql -u root -p -h 127.0.0.1
Enter password: 
...
MariaDB [(none)]>
```

#### Accediendo a servidor de base de datos desde el exterior  

En el ejemplo anterior hemos accedido a la base de datos de dos formas:
1. Ejecutado un comando bash para acceder al contenedor y desde dentro hemos utilizado el cliente de MariaDB para acceder a la base de datos.
2. Ejecutando directamente en el contenedor el cliente de MariaDB.  

En esta ocasión vamos a mapear los puertos para acceder desde el exterior a la base de datos:
1. Lo primero que vamos a hacer es eliminar el contenedor anterior: `$ docker rm -f mimariadb`
2. Y a continuación vamos a crear otro contenedor, pero en esta ocasión vamos a mapear el puerto 3306/tcp del Host Docker con el puerto 3306/tcp del contenedor:
```
$ docker run -d -p 3306:3306 --name mimariadb -e MARIADB_ROOT_PASSWORD=my-secret-pw mariadb:10.5
```

Comprobamos que los puertos se han mapeado y que el contenedor está ejecutándose:
```
$ docker ps
CONTAINER ID   IMAGE       COMMAND                  CREATED          STATUS          PORTS                                       NAMES
8d1857ff1d2f   mariadb     "docker-entrypoint.s…"   14 seconds ago   Up 11 seconds   0.0.0.0:3306->3306/tcp, :::3306->3306/tcp   mimariadb
```

Ahora desde nuestro equipo, donde hemos instalado un cliente de MariaDB (sudo apt install mariadb-client), nos conectamos al Host Docker:
```
$ mysql -u root -p -h 127.0.0.1
Enter password: 
...
MariaDB [(none)]>
```

### Etiquetando los contenedores con Labels  

Las etiquetas son un mecanismo para guardar metadatos en los objetos Docker: en contenedores, imágenes, volúmenes, redes, etc. Podemos utilizar etiquetas para organizar los distintos objetos Docker que estemos utilizando.  

Una etiqueta es una información del tipo clave-valor, almacenado como una cadena. Puede especificar varias etiquetas para un objeto, pero cada clave debe ser única dentro de un objeto.  

Para etiquetar un contenedor en su creación utilizaremos el parámetro -l (--label). Vamos a crear varios contenedores con distintas etiquetas:
```
$ docker run -l servicio=web -l entorno=desarrollo -l aplicacion=apache --name prueba_web ubuntu
$ docker run -l servicio=bd -l entorno=desarrollo -l aplicacion=mysql --name prueba_bd ubuntu
$ docker run -l servicio=web -l entorno=produccion --name web ubuntu
$ docker run -l servicio=bd -l entorno=produccion --name bd ubuntu

$ docker ps -a
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS                      PORTS     NAMES
6b5742b82a07   ubuntu    "/bin/bash"   7 seconds ago    Exited (0) 5 seconds ago              bd
30d6f1a83749   ubuntu    "/bin/bash"   19 seconds ago   Exited (0) 17 seconds ago             web
3d2ebb7ecfde   ubuntu    "/bin/bash"   39 seconds ago   Exited (0) 36 seconds ago             prueba_bd
553675a1457e   ubuntu    "/bin/bash"   52 seconds ago   Exited (0) 50 seconds ago             prueba_web
```

Hay que tener en cuenta que estos contenedores tendrán además de las etiquetas indicadas en su creación, las etiquetas que estén definidas en la imagen que hemos utilizado para su creación.  

A la hora de listar los contenedores podemos filtrar por varios criterios, entre ellos podemos usar las etiquetas para hacer el filtro.  

Por ejemplo, mostrar los contenedores que tienen una etiqueta aplicacion: `$ docker ps -a --filter="label=aplicacion"`  

Mostrar los contenedores que tienen la etiqueta entorno con el valor produccion: `$ docker ps -a --filter="label=entorno=produccion"`  

Por último, mostrar los contenedores cuyo servicio es web en el entorno de producción: `$ docker ps -a --filter="label=entorno=produccion" --filter="label=servicio=web"`   

Para terminar este apartado veamos un filtro que nos devuelve las etiquetas usando el comando docker inspect, por ejemplo:
```
$ docker inspect --format '{{range $key, $value := .Config.Labels}}{{$key}}: {{$value}}{{"\n"}}{{end}}' prueba_web
aplicacion: apache
entorno: desarrollo
org.opencontainers.image.ref.name: ubuntu
org.opencontainers.image.version: 22.04
servicio: web
```

Como observamos, este contenedor tiene 5 etiquetas, las tres que hemos indicado en su creación, y dos definidas en la imagen ubuntu.
