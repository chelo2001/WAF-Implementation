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

