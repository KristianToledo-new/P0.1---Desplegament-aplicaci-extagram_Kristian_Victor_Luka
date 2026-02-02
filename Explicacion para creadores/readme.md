# Projecte

# Inicio
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
- 
## Creacion de VPC
<img width="1181" height="226" alt="image" src="https://github.com/user-attachments/assets/9678c82f-bf01-4a9b-9687-486379ccaa6a" />
Se muestra la creacion de la instancia inicial para poder comenzar con el trabajo.

### 1.1 Creacion y configuracion de instancia del S2

<img width="730" height="566" alt="image" src="https://github.com/user-attachments/assets/f1f87f87-8009-44be-8abd-3f78ffd717cd" />

Se confirma la creación de la VPC-Extagram-vpc con el direccionamiento IP 10.0.0.0/16, estableciendo la red privada virtual del proyecto

-Instancia está creada.
<img width="741" height="348" alt="image" src="https://github.com/user-attachments/assets/fd0a5ce0-2340-41bb-a0bf-9099c5fa3595" />

Volvemos a confirmar la si la instancia está creada.

-Iniciacion.
<img width="746" height="178" alt="image" src="https://github.com/user-attachments/assets/afe4acc4-c57d-4743-98c2-6d0cac48e480" />

Seguridad de clave: Se usa chmod 400 para proteger la clave privada .pem, permitiendo que AWS la acepte para la conexión.
Comando de entrada: Se ejecuta ssh -i para conectar con el usuario ubuntu en la dirección IP del servidor dinámico S2.
Verificación: El sistema pide confirmar la huella digital (fingerprint) de la clave para asegurar que el destino es el correcto.
Inicio de sesión: Tras confirmar con un "yes", se obtiene acceso a la terminal remota para configurar Nginx o PHP-FPM.

## Instalación de servicios.
Instalacion del ngix y php:

<img width="672" height="291" alt="image" src="https://github.com/user-attachments/assets/040acaa9-6da5-45c5-827b-041301fd37f5" />

Comando de instalación: Se utiliza sudo apt install para descargar e instalar simultáneamente Nginx, PHP-FPM y el módulo PHP-MySQL.
Gestión de dependencias: El sistema identifica automáticamente los paquetes necesarios, como php8.3-fpm, para ejecutar la parte dinámica del proyecto.
Preparación del entorno: Esta acción prepara al servidor S2 para procesar el script extagram.php y conectar con la base de datos S7.
Progreso técnico: La captura confirma que se están descargando 5676 kB de archivos desde los repositorios oficiales de Ubuntu para activar la infraestructura web.

Arranque de los servicios

<img width="659" height="135" alt="image" src="https://github.com/user-attachments/assets/e296abd7-8cea-49d1-bb70-5a00ef6a6c5f" />

Esta captura muestra la habilitación y arranque inmediato de los servicios Nginx y PHP 8.3-FPM en el servidor mediante el comando systemctl, asegurando que se inicien automáticamente con el sistema.

Comprobamos estatus Nginx

<img width="665" height="200" alt="image" src="https://github.com/user-attachments/assets/c31a935c-641f-4b18-8a79-3d89bba58ca9" />

Se habilitan y arrancan los servicios PHP 8.3-FPM y Nginx mediante systemctl para que funcionen inmediatamente y se inicien automáticamente al arrancar el servidor.
Comprobamos estatus PHP

<img width="665" height="200" alt="image" src="https://github.com/user-attachments/assets/704f90a8-cc21-4e56-a15d-6e7a3c2792f5" />

