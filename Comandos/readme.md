## Índice
- [Scripts](#Scripts)
- [Instalación de servicios del servidor 1](#Instalación-de-servicios-del-servidor-1)
- [Instalación de servicios del servidor 2](#instalacion-de-servicios-del-servidor-2)
- [Instalación de servicios del servidor 3](#instalacion-de-servicios-del-servidor-3)
- [Instalación de servicios del servidor 4](#instalacion-de-servicios-del-servidor-4)
- [Instalación de servicios del servidor 5](#instalacion-de-servicios-del-servidor-5)
- [Instalación de servicios del servidor 6](#instalacion-de-servicios-del-servidor-6)
- [Instalación de servicios del servidor 7](#instalacion-de-servicios-del-servidor-7)

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
