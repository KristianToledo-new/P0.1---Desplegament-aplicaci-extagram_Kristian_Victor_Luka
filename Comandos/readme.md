## Índice
- [Scripts](#Scripts)
- [Instalación de servicios del servidor 1](#Instalación-de-servicios-del-servidor-1)
- [Instalación de servicios del servidor 2](#Instalación-de-servicios-del-servidor-2)
- [Instalación de servicios del servidor 3](#Instalación-de-servicios-del-servidor-3)
- [Instalación de servicios del servidor 4](#Instalación-de-servicios-del-servidor-4)
- [Instalación de servicios del servidor 5](#Instalación-de-servicios-del-servidor-5)
- [Instalación de servicios del servidor 6](#Instalación-de-servicios-del-servidor-6)
- [Instalación de servicios del servidor 7](#Instalación-de-servicios-del-servidor-7)
## Scripts.
extagram.php:
```bash
<!DOCTYPE html>
<link rel="stylesheet" href="https://static.extagram.itb/style.css">
 
<form method="POST" enctype="multipart/form-data" action="upload.php">
	<input type="text" name="post" placeholder="Write something...">
	<input id="file" type="file" name="photo" onchange="document.getElementById('preview').src=window.URL.createObjectURL(event.target.files[0])">
	<label for="file">
                	 <img id="preview" src="https://static.extagram.itb/preview.svg">
	</label>
	<input type="submit" value=”Publish”>
</form>
<?php
$db = new mysqli("db.extagram.itb", "extagram_admin", "pass123", "extagram_db");
 
foreach ($db->query("SELECT * FROM posts") as $fila) {
                	echo "<div class='post'>";
                	echo "<p>".$fila['post']."</p>";
                	if (!empty($fila['photourl'])) {
	            	    echo "<img src='https://storage.extagram.itb/".$fila['photourl']."'>";
                	}
                	echo "</div>";
}
?>
```

preview.svg:
```bash
&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;
&lt;svg version=&quot;1.1&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot; viewBox=&quot;0 0 100 100&quot; width=&quot;300&quot; height=&quot;300&quot;&gt;
&lt;g&gt;
&lt;rect width=&quot;100&quot; height=&quot;100&quot; fill=&quot;#cecece&quot;/&gt;
&lt;path fill=&quot;#ffffff&quot; transform=&quot;translate(25 25)&quot; d=&quot;M48.1,26.3c0,4.3,0,7.2-0.1,8.8c-0.2,3.9-1.3,6.9-3.5,9s-5.1,3.3-9,3.5c-
1.6,0.1-4.6,0.1-8.8,0.1c-4.3,0-7.2,0-8.8-0.1 c-3.9-0.2-6.9-1.3-9-3.5c-2.1-2.1-3.3-5.1-3.5-9c-0.1-1.6-0.1-4.6-0.1-8.8s0-
7.2,0.1-8.8c0.2-3.9,1.3-6.9,3.5-9 c2.1-2.1,5.1-3.3,9-3.5c1.6-0.1,4.6-0.1,8.8-
0.1c4.3,0,7.2,0,8.8,0.1c3.9,0.2,6.9,1.3,9,3.5s3.3,5.1,3.5,9 C48,19.1,48.1,22,48.1,26.3z M28.8,8.7c-1.3,0-2,0-2.1,0c-
0.1,0-0.8,0-2.1,0c-1.3,0-2.3,0-2.9,0c-0.7,0-1.6,0-2.7,0.1 c-1.1,0-2.1,0.1-2.9,0.3c-0.8,0.1-1.5,0.3-2,0.5c-0.9,0.4-1.7,0.9-
2.5,1.6c-0.7,0.7-1.2,1.5-1.6,2.5c-0.2,0.5-0.4,1.2-0.5,2 s-0.2,1.7-0.3,2.9c0,1.1-0.1,2-
0.1,2.7c0,0.7,0,1.7,0,2.9c0,1.3,0,2,0,2.1s0,0.8,0,2.1c0,1.3,0,2.3,0,2.9c0,0.7,0,1.6,0.1,2.7
c0,1.1,0.1,2.1,0.3,2.9s0.3,1.5,0.5,2c0.4,0.9,0.9,1.7,1.6,2.5c0.7,0.7,1.5,1.2,2.5,1.6c0.5,0.2,1.2,0.4,2,0.5
c0.8,0.1,1.7,0.2,2.9,0.3s2,0.1,2.7,0.1c0.7,0,1.7,0,2.9,0c1.3,0,2,0,2.1,0c0.1,0,0.8,0,2.1,0c1.3,0,2.3,0,2.9,0
c0.7,0,1.6,0,2.7-0.1c1.1,0,2.1-0.1,2.9-0.3c0.8-0.1,1.5-0.3,2-0.5c0.9-0.4,1.7-0.9,2.5-1.6c0.7-0.7,1.2-1.5,1.6-2.5 c0.2-
0.5,0.4-1.2,0.5-2c0.1-0.8,0.2-1.7,0.3-2.9c0-1.1,0.1-2,0.1-2.7c0-0.7,0-1.7,0-2.9c0-1.3,0-2,0-2.1s0-0.8,0-2.1 c0-1.3,0-2.3,0-
2.9c0-0.7,0-1.6-0.1-2.7c0-1.1-0.1-2.1-0.3-2.9c-0.1-0.8-0.3-1.5-0.5-2c-0.4-0.9-0.9-1.7-1.6-2.5 c-0.7-0.7-1.5-1.2-2.5-1.6c-
0.5-0.2-1.2-0.4-2-0.5c-0.8-0.1-1.7-0.2-2.9-0.3c-1.1,0-2-0.1-2.7-0.1C31.1,8.7,30.1,8.7,28.8,8.7z
M34.4,18.5c2.1,2.1,3.2,4.7,3.2,7.8s-1.1,5.6-3.2,7.8c-2.1,2.1-4.7,3.2-7.8,3.2c-3.1,0-5.6-1.1-7.8-3.2c-2.1-2.1-3.2-4.7-3.2-7.8
s1.1-5.6,3.2-7.8c2.1-2.1,4.7-3.2,7.8-3.2C29.7,15.3,32.3,16.3,34.4,18.5z M31.7,31.3c1.4-1.4,2.1-3.1,2.1-5s-0.7-3.7-2.1-5.1
c-1.4-1.4-3.1-2.1-5.1-2.1c-2,0-3.7,0.7-5.1,2.1s-2.1,3.1-2.1,5.1s0.7,3.7,2.1,5c1.4,1.4,3.1,2.1,5.1,2.1
C28.6,33.4,30.3,32.7,31.7,31.3z M39.9,13c0.5,0.5,0.8,1.1,0.8,1.8c0,0.7-0.3,1.3-0.8,1.8c-0.5,0.5-1.1,0.8-1.8,0.8 s-1.3-
0.3-1.8-0.8c-0.5-0.5-0.8-1.1-0.8-1.8c0-0.7,0.3-1.3,0.8-1.8c0.5-0.5,1.1-0.8,1.8-0.8S39.4,12.5,39.9,13z&quot;/&gt;
&lt;/g&gt;
&lt;/svg&gt;
```

style.css:
```bash
body {
	background: #fafafa;
	font-family: sans;
	margin: 0;
}
 form {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	gap: 1em;
	background: white;
	border-bottom: 1px solid #dbdbdb;
	padding: 8px;
}
 input[type=text] {
	border: 1px solid #dbdbdb;
	padding: 8px;
	width: 300px;
} 
input[type=submit] {
	background: #0096f7;
	color: white;
	border: 0;
	border-radius: 3px;
	width: 300px;
	padding: 8px;
} 
#file { display: none; }
 
#preview { max-width: 300px; }
 
.post {
	max-width: 600px;
	margin: 0 auto;
	background: white;
	display: flex;
	flex-direction: column;
	border: 1px solid #dbdbdb;
	border-radius: 3px;
	margin-bottom: 24px;
}
 
.post img { max-width: 600px; }
 
.post p { padding: 16px; }
```

upload.php:
```bash
<?php
if (!empty($_POST["post"])) {
 
	$photoid;
	if(!empty($_FILES['photo']['name'])){
    	$photoid = uniqid();
        move_uploaded_file($_FILES['photo']['tmp_name'], 'uploads/' . $photoid);
	}
	$db = new mysqli("db.extagram.itb", "extagram_admin", "pass123", "extagram_db");
	$stmt = $db->prepare("INSERT INTO posts VALUES(?,?)");
	$stmt->bind_param("ss", $_POST["post"], $photoid);
	$stmt->execute();
	$stmt->close();
}
 
header("location: /");
?>
```



## Instalación de servicios del servidor 1.
Instalacion del ngix y php:
```bash
sudo apt install -y nginx php-fpm php-mysql
```
Arranque de servicios:
```bash
sudo systemctl enable --now php8.3-fpm
sudo systemctl enable --now nginx
```
Comprobamos estatus NGINX:
```bash
systemctl status nginx
```
Comprobamos estatus PHP:
```bash
sudo systemctl status php8.3-fpm --no-pager
```
Verificamos Socket:
```bash
ls -l /run/php/
```

Ajustamos NGINX para usar el socket que queremos:
```bash
location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/run/php/php8.3-fpm.sock;
}
```
```bash
sudo nginx -t
sudo systemctl reload nginx
```

##Creacion de pagina web.
Creamos la carpeta de nuestra web:
```bash
sudo mkdir -p /var/www/extagram
sudo chown -R www-data:www-data /var/www/extagram
```
Crear extagram.php (Version de prueba):
```bash
<?php
echo "<h1>Extagram backend</h1>";
echo "<p>Servidor: " . gethostname() . "</p>";
echo "<p>Hora: " . date("H:i:s") . "</p>";
?>
```
Creamos el site de NGINX:
```bash
server {
    listen 80;
    server_name _;

    root /var/www/extagram;
    index extagram.php;

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

## Instalación de servicios del servidor 2.
Instalacion del ngix y php:
```bash
sudo apt install -y nginx php-fpm php-mysql
```

## Instalación de servicios del servidor 3.
Instalacion del ngix y php:
```bash
sudo apt install -y nginx php-fpm php-mysql
```

## Instalación de servicios del servidor 4.
Instalacion del ngix y php:
```bash
sudo apt install -y nginx php-fpm php-mysql
```

## Instalación de servicios del servidor 5.
Instalacion del ngix y php:
```bash
sudo apt install -y nginx php-fpm php-mysql
```

## Instalación de servicios del servidor 6.
Instalacion del ngix y php:
```bash
sudo apt install -y nginx php-fpm php-mysql
```

## Instalación de servicios del servidor 7.
Instalacion del ngix y php:
```bash
sudo apt install -y nginx php-fpm php-mysql
```
