## 1. Arquitectura General
La arquitectura S1–S2–S3 implementa una capa de entrada con alta disponibilidad mediante un Application Load Balancer (S1) y dos servidores backend idénticos (S2 y S3) que ejecutan PHP-FPM y NGINX. El balanceador distribuye el tráfico HTTP entre ambos nodos para garantizar tolerancia a fallos y escalabilidad.

## 2. Servidor S1 – Application Load Balancer (ALB)
S1 actúa como proxy inverso y balanceador de carga. Está configurado como 'internet-facing' y escucha en el puerto 80. Recibe todas las peticiones HTTP de los clientes y las reenvía al Target Group TG-Extagram.

# Configuración principal:
- Tipo: Application Load Balancer
- Listener: HTTP 80
- Target Group: TG-Extagram
- Health Check: /health
- Security Group: SG-ALB-Extagram (permite HTTP 80 desde 0.0.0.0/0)

El ALB distribuye las peticiones entre S2 y S3 utilizando Round-Robin.

## 3. Servidor S2 – Backend PHP-FPM + NGINX
S2 es una instancia EC2 Ubuntu que ejecuta NGINX como servidor web y PHP-FPM para la parte dinámica. Aloja el script extagram.php que muestra el hostname y la hora para comprobar el balanceo.

# Servicios instalados:
- nginx
- php8.3-fpm

Socket PHP-FPM: /run/php/php8.3-fpm.sock

# Configuración NGINX:
```bash
server {
    listen 80;
    root /var/www/extagram;
    index extagram.php;

    location = /health {
        return 200 "OK";
    }

    location / {
        try_files $uri $uri/ /extagram.php;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_pass unix:/run/php/php8.3-fpm.sock;
    }
}

```
Este servidor responde a las peticiones reenviadas por S1 y es supervisado por el health check.

## 4. Servidor S3 – Backend clonado
S3 es una réplica exacta de S2 creada a partir de una AMI. Posee la misma configuración de NGINX, PHP-FPM y el mismo código de extagram.php.
Su función es proporcionar alta disponibilidad. Si S2 falla, el ALB redirige automáticamente todo el tráfico hacia S3.
Ambos servidores están registrados en el mismo Target Group y comparten el mismo Security Group SG-WEB-Extagram.

## 5. Alta Disponibilidad y Balanceo
Con S2 y S3 en estado Healthy, el ALB reparte las peticiones de forma automática. Al refrescar la página del ALB se observa el cambio de hostname entre nodos, demostrando el balanceo.
En caso de detener NGINX en uno de los servidores, el ALB deja de enviarle tráfico y continúa sirviendo peticiones con el nodo restante, garantizando continuidad del servicio.
