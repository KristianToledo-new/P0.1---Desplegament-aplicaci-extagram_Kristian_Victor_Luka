Extagram es una aplicación web sencilla inspirada en Instagram que permite a los usuarios escribir mensajes cortos y subir fotos que todos pueden ver en tiempo real. Imagina una red social básica donde cualquiera puede publicar contenido y el resto lo visualiza inmediatamente. Este proyecto consiste en montar toda la infraestructura técnica para que funcione de manera rápida, estable y sin interrupciones, incluso si alguna parte falla.

##Qué hace exactamente la aplicación
Cuando un usuario entra en la web, ve un formulario muy simple:

Un campo de texto donde escribe su mensaje ("¡Hola mundo!" o lo que quiera)

Un botón para seleccionar una foto desde su ordenador

Una vista previa de la foto que ha elegido (antes de publicarla)

Un botón "Publicar" que envía todo al servidor

Al pulsar Publicar:

La foto se guarda en una carpeta especial del servidor

El texto y el nombre del archivo de la foto se guardan en una base de datos MySQL

La página se recarga y muestra el nuevo post junto con todos los anteriores

Todos los usuarios ven los mismos posts en orden cronológico, con el texto encima de cada foto.

La arquitectura explicada como un equipo de trabajo
Piensa en la web como una empresa con diferentes departamentos especializados, todos conectados por una red interna:

S1 - El Recepcionista Principal (NGINX Proxy)
Recibe todas las visitas que llegan desde internet. No hace el trabajo pesado, solo decide a quién enviar cada petición:

Si alguien quiere ver los posts → envía a S2 o S3 (balanceo de carga)

Si alguien sube foto → envía a S4

Si alguien pide una foto → envía a S5

Si pide estilos CSS → envía a S6

S2 y S3 - Los Mostradores PHP (PHP-FPM)
Son dos trabajadores idénticos que ejecutan el archivo extagram.php. Este archivo:

Se conecta a la base de datos MySQL

Lee todos los posts

Muestra el HTML con textos e imágenes

Tienen réplicas porque si uno falla, el otro sigue atendiendo

S4 - El Almacén de Subidas (PHP-FPM)
Ejecuta upload.php que recibe el formulario:

Genera un nombre único para la foto (con uniqid())

Guarda la foto físicamente en /uploads/

Inserta texto + nombre_foto en MySQL

Redirige de vuelta a la página principal

S5 - El Repartidor de Fotos (NGINX Estático)
Sirve solo las fotos desde la carpeta /uploads/. Es súper rápido porque NGINX sirve archivos estáticos sin procesar PHP.

S6 - Repartidor de Estilos (NGINX Estático)
Sirve style.css y preview.svg. Separa los recursos estáticos del contenido dinámico.

S7 - La Base de Datos (MySQL)
Guarda en la tabla posts:

text
post (TEXT)        | photourl (TEXT)
"Hola mundo"       | "abc123.jpg"
"Mi foto"          | "def456.png"
Por qué tantos servidores separados
Alta Disponibilidad: Si S2 falla, S1 envía todo a S3. Si S4 está ocupado, espera. Si S5 no responde, en fases futuras la BBDD puede servir las fotos como blobs.

Escalabilidad: Puedes añadir más S2/S3 si hay mucha gente viendo posts, más S4 si suben muchas fotos.

Seguridad: Cada servicio solo hace una cosa. Si hackean el visor de posts, no pueden subir archivos.

Rendimiento: NGINX es rapidísimo sirviendo fotos/estilos. PHP solo procesa lógica. MySQL solo guarda datos.

Fases del proyecto paso a paso
FASE 1 - Versión Básica (1 servidor)
Todo funciona en una sola máquina:

text
[ NGINX + PHP + MySQL + uploads/ ]
Repasas configuración básica de servidor web, PHP-FPM, MySQL. Subir foto → funciona. Ver posts → funciona.

FASE 2 - Dockerización Completa
Separas todo en 7 contenedores Docker conectados por red puente:

text
Internet → [S1 NGINX] → [S2 PHP] [S3 PHP]
                    ↘ [S4 Upload] → [uploads/]
                    ↘ [S5 Fotos] 
                    ↘ [S6 CSS/SVG]
                    ↘ [S7 MySQL]
FASE 3 - Pruebas de Resistencia

Crear 10 posts con fotos → OK

Parar S2 → S3 sigue sirviendo posts

Parar S5 → ¿Las fotos siguen visibles? (futuro: desde MySQL)

Sobrecarga de subida → S1 balancea correctamente

Beneficios para el cliente final
✅ Nunca cae: Siempre hay servidores de respaldo
✅ Rápido: Cada parte optimizada para su función
✅ Escala fácil: Añade más contenedores según necesites
✅ Mantenible: Problema en fotos ≠ problema en base de datos
✅ Económico: Docker usa pocos recursos

Estado actual del proyecto
Ya tienes:

✅ Código PHP funcional (extagram.php, upload.php)

✅ Esquema MySQL creado

✅ CSS y preview.svg listos

✅ GitHub repository iniciado

⏳ Pendiente: Dockerizar + arquitectura completa S1-S7

El resultado final será una web profesional que podría soportar miles de usuarios diarios, exactamente como las grandes plataformas sociales.
