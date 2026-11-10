## Instalación de herrammientas
Primero se comenzarán instalando las herramientas necesarias para la implementación del servidor web. En este caso se utilizará un servior web apache, por lo que se requerirá instalar dicho servidor, el lenguaje de back-end a utilizar (php en este caso), los conectores para la comunicación entre el lenguaje de programación y la base de datos y el propio servidor de base de datos. Esto se hace con el siguiente comando.

```bash
sudo apt-get install -y apache2 php php-mysql mysql-server
```
Luego se recomienda ejecutar el siguiente comando, el cual permite establecer una contraseña para el usuario root en el servidor de base de datos, además de proporcionar otras capas de seguridad.

```bash
sudo mysql_secure_installation
```



## Configuración de la aplicación web vulnerable
Primero se debe clonar el repositorio de github de la app vulnerable.
```bash
cd /var/www/html
sudo git clone https://github.com/digininja/DVWA.git
```
Si no se tiene git instalado, se debe instalar con el siguiente comando;
```bash
sudo apt-get install -y git
```
Ahora se debe cambiar el propietario del directorio DVWA y dejar al usuario www-data. además de otorgarle los permisos necesarios a dicho usuario en ese directorio.
```bash
sudo chown -R www-data:www-data DVWA
sudo chmod -R 755 DVWA
```
Ahora se debe editar el archivo de configuración de la aplicación web ubicado en la ruta DVWA/config/config.inc.php y actualizar los valores de las variables a los de la tabla.

<div align="center">

| Variable | Valor |
|:--------:|:-----:|
| `$DBMS`  | `MySQL` |
| `$db`    | `dvwa` |
| `$user`  | `dvwa_user` |
| `$pass`  | `p@ssw0rd` |
| `$host`  | `localhost` |

</div>

Luego se debe crear una nueva base de datos y un nuevo usuario en el servidor de base de datos mysql al que se le otorgarán todos los permisos en la base de datos creada anteriormente (DVWA) y se le concederán a nivel local.

```bash
sudo mysql -u root -p
CREATE DATABASE dvwa;
CREATE USER 'dvwa_user'@'localhost' IDENTIFIED BY 'p@ssw0rd';
GRANT ALL ON dvwa.* TO 'dvwa_user'@'localhost';
FLUSH PRIVILEGES;
exit;
```
Ahora se debe navegar a http://<Ubuntu IP>/DVWA/setup.php y clickear en resetear base de datos.




