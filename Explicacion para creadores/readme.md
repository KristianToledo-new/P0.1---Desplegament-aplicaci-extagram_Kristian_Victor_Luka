# Projecte

# Inicio

<img width="566" height="664" alt="image" src="https://github.com/user-attachments/assets/422ae6d5-b4bc-474e-9f07-bc4625cf3a69" />

<img width="567" height="369" alt="image" src="https://github.com/user-attachments/assets/e63238a4-ae1c-46b2-bf31-1d84f3dee38d" />

Primero de todo esta imagen representa la arquitectura lógica y el flujo de datos de tu proyecto Extagram. Es el mapa de cómo viaja la información desde que el usuario entra en la web hasta que se guardan sus fotos o datos.
Aquí tienes el resumen completo de lo que hemos hecho hasta ahora, uniendo la configuración real en AWS con la simulación que estamos montando:

## La Idea del Packet Tracer
El objetivo de Packet Tracer es crear una "maqueta" visual y funcional de la infraestructura que estamos desplegando en la nube. Mientras que en AWS todo son menús y comandos, aquí hemos diseñado el esquema físico para entender cómo fluyen los datos:

El Router: Representa nuestra salida a Internet y la puerta de enlace de la VPC.

El Switch: Es el corazón de nuestra red local que conecta todos los servidores.

Los Servidores (S1-S7): Cada uno cumple la función específica que definimos en el diagrama de arquitectura (Balanceador, App, DB, etc.).

## Todo lo que hemos hecho (paso a paso)
Preparación del Entorno: Hemos creado la estructura de directorios en el servidor y hemos ajustado los permisos para que el usuario www-data pueda trabajar sin restricciones.

Configuración del Backend: Hemos programado el archivo extagram.php para que nos devuelva el nombre de la instancia y la hora, permitiéndonos verificar qué servidor está respondiendo en cada momento.

Conexión Nginx-PHP: Hemos configurado Nginx para que se comunique con el motor PHP a través de un socket, hemos validado que no hubiera errores y hemos reiniciado el servicio.

Control de Salud (Health Check): Hemos creado una ruta específica (/health) que responde con un "OK". Hemos configurado el balanceador de AWS para que use esta ruta y sepa si el servidor está "sano" antes de enviarle tráfico.

Escalabilidad y Clonación: Hemos generado una imagen de Amazon (AMI) de nuestro servidor S2 ya configurado. Gracias a esto, hemos lanzado la instancia S3 y hemos comprobado que funciona exactamente igual que la anterior sin tener que repetir todo el trabajo.

Simulación Física: Hemos conectado todos los dispositivos en Packet Tracer usando el cableado automático y hemos empezado a asignar las direcciones IP fijas a cada servidor para que la red sea idéntica a la de AWS.

# Guía de Inicio: Proyecto Extagram

Esta guía detalla los pasos iniciales y las opciones técnicas para el despliegue de una aplicación web de alta disponibilidad y escalabilidad.
## Gestión y Control de Versiones
Antes de iniciar el desarrollo técnico, es obligatorio configurar el entorno de colaboración:

-GitHub: Se debe crear un repositorio central. El acceso al servidor se realizará mediante intercambio de claves pública/privada.

-ProofHub: Herramienta obligatoria para la planificación y gestión de tareas. Es necesario adjuntar capturas de pantalla de esta herramienta en las actas de cada sprint.

-Documentación MD: Toda la documentación, incluyendo las actas de las reuniones (sprint planning y sprint review), debe estar en formato Markdown dentro del repositorio.
## Opciones de Despliegue y Arquitectura
El proyecto se divide en fases evolutivas para asegurar el aprendizaje de la infraestructura:

-Opción A: Monolítica (Sprint 1)	
Instalación de NGINX o Apache en una sola máquina.

Repasar la configuración de módulos y servicios básicos.

-Opción B: Segregada (Sprints 2 y 3)	
Uso de Docker para separar la aplicación en 7 servidores distintos.

Simular un entorno real de alta disponibilidad con balanceo de carga.
## Componentes de la Infraestructura (S1-S7)
-S1 (Proxy/Balanceador): Servidor Nginx que recibe todas las peticiones y realiza un balanceo de carga entre S2 y S3.

-S2 y S3 (App Servers): Servicios PHP-FPM encargados de ejecutar el script dinámico extagram.php.

-S4 (Upload Server): Servicio PHP-FPM que ejecuta upload.php para almacenar imágenes en el servidor.

-S5 y S6 (Static Servers): Servidores Nginx para servir imágenes (S5) y archivos de estilo o gráficos como style.css y preview.svg (S6).

-S7 (Base de Datos): Servidor MySQL que almacena la información y replica archivos como "blobs" por seguridad.
## Configuración Inicial de la Base de Datos
Para el primer despliegue funcional, se debe utilizar el siguiente esquema:

-Base de datos: extagram_db.
-Usuario: extagram_admin con contraseña pass123.
-Tabla inicial: posts con columnas para el texto del post y la URL de la fotografía.
# **AP - P0.1---Despliegue-aplicacin-extagram - Grupo 4** 


## Miembros del equipo 

- Kristian Toledo
- Luka ukleba
- Victor Serrano

## Índice
- [Creacion de VPC](#Creacion-de-VPC)
- [Instalación de servicios.](#Instalación-de-servicios.)
- [Creación de S2](#Creación-de-S2)
- [Creación de S3](#Creación-de-S3)
- [Creación de S4](#Creacion-de-s4)

## Creacion de VPC
<img width="1181" height="226" alt="image" src="https://github.com/user-attachments/assets/9678c82f-bf01-4a9b-9687-486379ccaa6a" />
Se muestra la creacion de la instancia inicial para poder comenzar con el trabajo.

# Creación de S2
<img width="730" height="566" alt="image" src="https://github.com/user-attachments/assets/f1f87f87-8009-44be-8abd-3f78ffd717cd" />

Se confirma la creación de la VPC-Extagram-vpc con el direccionamiento IP 10.0.0.0/16, estableciendo la red privada virtual del proyecto

## Instancia está creada.

<img width="741" height="348" alt="image" src="https://github.com/user-attachments/assets/fd0a5ce0-2340-41bb-a0bf-9099c5fa3595" />

Volvemos a confirmar la si la instancia está creada.

## Iniciación.

<img width="746" height="178" alt="image" src="https://github.com/user-attachments/assets/afe4acc4-c57d-4743-98c2-6d0cac48e480" />

Seguridad de clave: Se usa chmod 400 para proteger la clave privada .pem, permitiendo que AWS la acepte para la conexión.
Comando de entrada: Se ejecuta ssh -i para conectar con el usuario ubuntu en la dirección IP del servidor dinámico S2.
Verificación: El sistema pide confirmar la huella digital (fingerprint) de la clave para asegurar que el destino es el correcto.
Inicio de sesión: Tras confirmar con un "yes", se obtiene acceso a la terminal remota para configurar Nginx o PHP-FPM.

# Instalación de servicios.
## Instalacion del ngix y php:

<img width="672" height="291" alt="image" src="https://github.com/user-attachments/assets/040acaa9-6da5-45c5-827b-041301fd37f5" />

Comando de instalación: Se utiliza sudo apt install para descargar e instalar simultáneamente Nginx, PHP-FPM y el módulo PHP-MySQL.
Gestión de dependencias: El sistema identifica automáticamente los paquetes necesarios, como php8.3-fpm, para ejecutar la parte dinámica del proyecto.
Preparación del entorno: Esta acción prepara al servidor S2 para procesar el script extagram.php y conectar con la base de datos S7.
Progreso técnico: La captura confirma que se están descargando 5676 kB de archivos desde los repositorios oficiales de Ubuntu para activar la infraestructura web.

## Arranque de los servicios

<img width="659" height="135" alt="image" src="https://github.com/user-attachments/assets/e296abd7-8cea-49d1-bb70-5a00ef6a6c5f" />

Esta captura muestra la habilitación y arranque inmediato de los servicios Nginx y PHP 8.3-FPM en el servidor mediante el comando systemctl, asegurando que se inicien automáticamente con el sistema.

## Comprobamos estatus Nginx

<img width="665" height="200" alt="image" src="https://github.com/user-attachments/assets/c31a935c-641f-4b18-8a79-3d89bba58ca9" />

Se habilitan y arrancan los servicios PHP 8.3-FPM y Nginx mediante systemctl para que funcionen inmediatamente y se inicien automáticamente al arrancar el servidor.

## Comprobamos estatus PHP

<img width="665" height="200" alt="image" src="https://github.com/user-attachments/assets/704f90a8-cc21-4e56-a15d-6e7a3c2792f5" />

## Verificamos Socket

<img width="599" height="95" alt="Captura de pantalla 2026-02-02 115556" src="https://github.com/user-attachments/assets/7944ffa9-2ba5-46c2-9b3c-1a26186504b0" />

El comando ls -l /run/php/ comprueba la existencia del archivo socket (php8.3-fpm.sock), que es el "túnel" indispensable para que Nginx pueda enviarle las peticiones de la web a PHP para que las procese.

## Ajustamos NGINX para usar el socket que queremos

<img width="599" height="174" alt="image" src="https://github.com/user-attachments/assets/a98e256e-7f9c-434f-8ff7-122bc235395b" />

Esta imagen muestra la configuración final de enlace entre el servidor web y el motor de PHP. Aquí tienes la explicación en una frase:
Se edita el archivo de sitio en Nginx para que redirija las peticiones .php al socket de PHP 8.3-FPM, verificando después que la sintaxis es correcta con nginx -t y aplicando los cambios con un reload.

## Comprobamos que funciona nuestro NGINX con nuestra IP publica

<img width="601" height="217" alt="image" src="https://github.com/user-attachments/assets/f3eacd19-3111-4329-b2c9-cccd97dacbdb" />

# Creacion de pagina web
## Creamos la carpeta de nuestra web

<img width="596" height="47" alt="image" src="https://github.com/user-attachments/assets/fe2cb038-ca77-4df0-b9ce-d336b9d3f62d" />

Hemos creado la carpeta del proyecto y le he dado la propiedad al usuario www-data para que el servidor web pueda gestionar los archivos sin problemas de permisos y luego he configurado la conexión entre Nginx y PHP, verificado que no cometí errores de sintaxis y reiniciado el servicio para activar la web.

## Crear extagram.php (Version de prueba)

<img width="600" height="106" alt="image" src="https://github.com/user-attachments/assets/328da8a7-afe3-4064-a6f4-391525613d71" />

Hemos creado el archivo extagram.php dentro del directorio del proyecto, escribiendo un pequeño código que mostrará en pantalla el nombre del servidor y la hora actual para confirmar que el backend ya está vivo.

## Creamos el site de NGINX

<img width="593" height="234" alt="image" src="https://github.com/user-attachments/assets/bdeba23d-bdde-44cf-a0b4-69f8e188dcd2" />

Hemos configurado el archivo de sitio de Nginx para definir la ruta del proyecto (/var/www/extagram), establecer extagram.php como página principal y habilitar el procesamiento de PHP a través del socket de PHP 8.3-FPM.


## Nuestra página web (Momentánea)

<img width="615" height="146" alt="image" src="https://github.com/user-attachments/assets/f39104a1-a048-4847-bd41-4af703ce546c" />

# Metemos S2 detrás del Load Balancer (S1)
## Registrar S2 en el Target Group (TG-Extagram)

<img width="587" height="380" alt="image" src="https://github.com/user-attachments/assets/4bc3d4a9-4451-4467-82d2-3719c2adfc2e" />

<img width="594" height="197" alt="image" src="https://github.com/user-attachments/assets/37d3330a-b576-4b07-913a-3624c42cf0a4" />

Hemos registrado la instancia S2 dentro del grupo de destinos del balanceador de carga en AWS para que empiece a recibir tráfico real por el puerto 80.

## Crear endpoint /health en S2

<img width="601" height="77" alt="image" src="https://github.com/user-attachments/assets/69097896-862d-4208-97a2-1891c74d1f99" />

<img width="502" height="40" alt="image" src="https://github.com/user-attachments/assets/e3569911-1a29-403f-b981-19a8306a0111" />

Hemos configurado una ruta de salud (/health) en Nginx para que devuelva un código 200 OK y hemos verificado con el comando curl que el servidor responde correctamente, asegurando así que el balanceador de carga lo reconozca como un destino sano.

## Cambiamos el Health Check del Target Group

<img width="587" height="105" alt="image" src="https://github.com/user-attachments/assets/2b98f0ff-fda9-4949-8f97-241f0e72567c" />

Hemos definido en el balanceador de carga de AWS que la ruta oficial para verificar si el servidor está vivo es /health, estableciendo que tras 5 comprobaciones exitosas el sistema se marque como "en buen estado".

## Ahora nos funciona correctamente

<img width="592" height="101" alt="image" src="https://github.com/user-attachments/assets/79370aa8-cae5-443f-bb1c-06548ffe019c" />

# Creacion de S3
## Realizamos una imagen de la instantánea S2

<img width="604" height="388" alt="image" src="https://github.com/user-attachments/assets/ab21cc8c-6305-43de-b21c-3074c2affd78" />

<img width="598" height="335" alt="image" src="https://github.com/user-attachments/assets/5f254e22-8cc4-4212-9736-9d3b19300b10" />

Hemos solicitado la creación de una imagen (AMI) a partir de nuestra instancia S2 ya configurada, llamándola "AMI-Extagram-Backend-S2", con el objetivo de poder clonar este servidor exacto y lanzar la instancia S3 en cuestión de segundos.

## Tiempo de espera 

<img width="606" height="498" alt="image" src="https://github.com/user-attachments/assets/7567c3ea-3059-443b-8754-300f3702c9fb" />

Después de esperar unos minutos para que la imagen está habilitada, empezamos con la creación de la S3 en base a esa imagen

<img width="473" height="421" alt="image" src="https://github.com/user-attachments/assets/0230ffd7-8929-4b33-8ec4-6bd82e9534c8" />

## Instantanea creada

<img width="601" height="128" alt="image" src="https://github.com/user-attachments/assets/206ea590-9d35-4016-aef6-d83f4cd4ce50" />

## Conexión

<img width="598" height="497" alt="image" src="https://github.com/user-attachments/assets/474a73c7-c428-49fd-b81e-374ac24f54f7" />

Hemos accedido por SSH a la nueva instancia S3 (con IP 10.0.1.123) y hemos ejecutado un par de pruebas rápidas: primero confirmamos que la ruta de salud responde "OK" y luego verificamos que la web principal ya está funcionando, mostrando correctamente el nombre del servidor y la hora sincronizada.

## Registramos el S3 en el Grupo de destino

<img width="370" height="441" alt="image" src="https://github.com/user-attachments/assets/ffd689b9-a142-4f94-ae4c-edb3cd2e84b6" />

<img width="593" height="150" alt="image" src="https://github.com/user-attachments/assets/c473c4a4-f9fe-4a8b-9737-250106fefca4" />

# Prueba de tolerancia a fallos


<img width="498" height="47" alt="image" src="https://github.com/user-attachments/assets/566f2142-3819-486d-a64d-122f78cbad51" />

Vamos a nuestro S2 y apagamos el NGINX

<img width="596" height="242" alt="image" src="https://github.com/user-attachments/assets/10ffe884-6e77-4882-be64-9dd7b51614c5" />

Vemos el DNS del ALB y sigue funcionando, ya que responde a nuestro S3

## Creación de S4
