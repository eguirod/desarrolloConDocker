# INTRODUCCIÓN GENERAL
Venimos de:
* Infraestructuras **monolíticas**, plantillas de VMS.
* Tareas **cron** y **anacron**.
* Bash **scripts**.
* Monitorización proactiva (**NRPE** scripts, **Zabbizx** alerts, Nagios)
* Primeras herramientas como **cfengine**.
# AUTOMATIZACIÓN
## Definición y tipos
La **automatización** es una técnica, método, sistema o conjunto de procesos con el objetivo de reducir al **mínimo** la **intervención humana**.  
Diseño a alto nivel: pasos para automatizar un procesos o necesidad de la infra:
1. Identificación de **entradas** de información: hay que tener claro el flujo completo del proceso el que sea, saber en un alto nivel hasta dónde llegamos. Por ejemplo, tenemos la necesidad de agregar usuarioas en nuestra infra, damos de alta al usuario en la app que usemos, que nos pedirá una serie de datos del usuario y por ejemplo en nuestra empresa tenemos 3 roles, sistemas, desarrollo, marketing y cada uno tendrá una serie de permisos y tareas.
2. Generar un mecanismo de **disparador** (**trigger**) de la automatización. En el ejemplo sería generar un mecanismo que nos dispare la automatización, los procesos para que se cree el usuario, establezca los roles etc...
3. **Evaluar** la **entrada** de información: la automatización debe evaluar los datos introducidos para identificar qué hacer en función de ellos. Por ejemplo en nuestro caso en función del rol que debemos deberá dar unos permisos y tareas diferentes.
4. **Ejecutar** las **tareas** de la automatización.

**Tipos**:
* *Manual*: ingresar info + ejecutar disparador. Se lanzará de forma manual con los datos que tenga.
* *Programado*: tarea repetitiva. Tareas rutinarias que se repiten en el tiempo y se programan para que se hagan solas. Por ejemplo, en servidores Windows los reinicios del servidor.
* *Evento*: el trigger se dispara ante un problema (es típico en la monitorización proactiva). Por ejemplo, si hubiera un FS que estuviera a punto de llenarse, se lanzaría una automatización que liberara espacio.
* *Auto-servicio*: gestión automatizada de tickets. Por ejemplo, tener un portal que cuando el usuario tenga una necesidad concreta, este portal realice las tareas necesarias para solventarla.
## Beneficios de la automatización
* **Automatización manual**:
  * Reduce el tiempo en completar la tarea.
  * Menor esfuerzo para requerir información.
  * Repetible.
  * Herramientas: rundeck, ansible, comandos.
* **Automatización programada**:
  * Procesos mejorados y mejor definidos.
  * Mayor consistencia.
  * Más confiable.
  * Herramientas: rundeck, comandos, puppet (control infra TI), chef(control infra TI).
* **Automatización en eventos**:
  * Proactivo vs reactivo.
  * Mejora confianza.
  * Menor incidencias por atender, menos cambio de contexto.
  * Herramientas: zabbix, nagios, kibana...
* **Automatización en auto-servicios**:
  * Finalización de tareas mucho más rápidas.
  * Clientes finales más contentos.
  * Se reduce la carga de trabajo y se ahorra tiempo.
  * Herramientas: OTRS (gestión de tickets), Zammad(gestión de tickets), puppet, chef.
# ORQUESTACIÓN
## Definición y beneficios
La **orquestación** permite establecer un **control** y **auditoría** de las diferentes automatismos realizados en una **infra** IT.  

**¿Por qué orquestar?**
* *Mantenimiento centralizado*: permite tener un mayor control sobre qué hacemos, cómo lo hacemos y los resultados.
* *Auditoría*: podemos evaluar si el automatismo hace lo que debe o no, de forma de que si hay un error podamos corregirlo manualmente.
* *Mejora los flujos de trabajo*.
* *Portal de auto-servicios*, pudiendo delegar tareas de administración a personas que quizás no tenga los conocimientos.
## Elementos de orquestación
* **Runbooks**: conjunto de procedimientos automatizados. Por ejemplo, la gestión de agregar un usuario en un AD, los pasos que está automatizados serían los runbooks.
* **Workflows**: conjunto de *runbooks* conectados, dando solución extremo a extremo. Por ejemplo, tener un desarrollo y que tengamos "un botón" que nos permita desplegarla.
* **Pipelines**: usado para el desarrollo continúa del software, se utiliza para desarrollar infra como código.
## Tipos de orquestación
# CONCLUSIONES
