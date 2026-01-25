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
<!DOCTYPE html>
```

## Instalación de servicios del servidor 1.
Instalacion del ngix y php:
```bash
sudo apt install -y nginx php-fpm php-mysql
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
