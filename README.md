# 1 Práctica: Administración de Wordpress con la utilidad WP-CLI
En esta práctica vamos a realizar la administración de un sitio WordPress desde el terminal con la utilidad WP-CLI.

Con la utilidad WP-CLI podemos realizar las mismas tareas que se pueden hacer desde el panel de administración web de WordPress, pero desde la línea de comandos.

En la web oficial de WordPress podemos encontrar:

el manual de uso de WP-CLI
los comandos de WP-CLI.
### 1.1 Requisitos
La máquina donde vamos a instalar la utilidad WP-CLI será la misma máquina donde queremos realizar la instalación de WordPress y tendrá que tener instalado todo el software necesario de la pila LAMP.

## 1.2 Instalación de WP-CLI en el servidor LAMP
Descargamos el archivo wp-cli.phar del repositorio oficial de WP-CLI. Los archivos .phar son unos archivos similares a los archivos .jar de Java. Estos archivos se utilizan para distribuir aplicaciones o librerías de PHP en un único archivo. Puede encontrar más información sobre los archivos .phar en la documentación oficial de PHP.

curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
Le asignamos permisos de ejecución al archivo wp-cli.phar.

chmod +x wp-cli.phar
Movemos el archivo wp-cli.phar al directorio /usr/local/bin/ con el nombre wp para poder utilizarlo sin necesidad de escribir la ruta completa donde se encuentra.

sudo mv wp-cli.phar /usr/local/bin/wp
Una vez que hemos realizado el paso anterior podemos hacer uso de la utilidad desde la línea de comandos. Si escribimos wp en el terminal nos deberá mostrar la página de ayuda del comando.

wp
En la documentación oficial puede encontrar información más detallada sobre el proceso de instalación.

## 1.3 Ejemplo de uso: Instalación de WordPress con WP-CLI
Vamos a realizar un ejemplo de uso sobre una máquina que ya tiene instalado todo el software necesario de la pila LAMP.

### 1.3.1 Paso 1. Descarga del código fuente de WordPress (wp core download)
Nos situamos en el directorio donde queremos realizar la instalación de WordPress.

cd /var/www/html
Descargamos el código fuente de WordPress con el comando wp core download.

wp core download
Al ejecutar el comando anterior descargaremos el código fuente en el directorio actual. Con el parámetro --path es posible indicar el directorio donde queremos descargar el código fuente de WordPress. Por ejemplo:

wp core download --path=/var/www/html
También es posible seleccionar el idioma de WordPress, para que sólo se descargue el paquete del idioma que hemos elegido.

wp core download --locale=es_ES
Puede encontrar más información sobre el comando wp core download en la documentación oficial.

### 1.3.2 Paso 2. Creación del archivo de configuración (wp config create)
Antes de crear el archivo de configuración debemos crear en MySQL Server la base de datos, el usuario y la contraseña donde vamos a instalar WordPress.

Una vez que hemos creado la base de datos, usuario y contraseña en MySQL Server, podemos crear el archivo de configuración wp-config.php para WordPress con el siguiente comando:

wp config create --dbname=wordpress_db --dbuser=wordpress_user --dbpass=wordpress_password
En este paso le estamos indicando los siguientes parámetros:

--dbname=wordpress_db (Nombre de la base de datos)
--dbuser=wordpress_user (Usuario de la base de datos)
--dbpass=wordpress_password (Contraseña del usuario de la base de datos)
Tenga en cuenta que en su caso tendrá que reemplazar los valores: wordpress_db, wordpress_user y wordpress_password, por los valores que quiera utilizar para su base de datos, usuario y contraseña.

Al crear el archivo de configuración se crearán automáticamente los valores aleatorios para las security keys.

Puede encontrar más información sobre el comando wp config create en la documentación oficial.

### 1.3.3 Paso 3. Comprobación de los valores del archivo de configuración (wp config get)
Podemos comprobar los valores del archivo de configuración del archivo wp-config.php con el comando:

wp config get
El comando anterior nos devolverá la siguiente salida:

+-------------------+------------------------------------------------------------------+----------+
| name              | value                                                            | type     |
+-------------------+------------------------------------------------------------------+----------+
| table_prefix      | wp_                                                              | variable |
| DB_NAME           | wordpress_demo                                                   | constant |
| DB_USER           | wordpress_user                                                   | constant |
| DB_PASSWORD       | wordpress_password                                               | constant |
| DB_HOST           | localhost                                                        | constant |
| DB_CHARSET        | utf8                                                             | constant |
| DB_COLLATE        |                                                                  | constant |
| AUTH_KEY          | 4T-<=4yeO(9^Y/1-Cak7Y7w;I(hl*0C%(^Y4}j1((J.Bjy^F^.p3RuI>[9G-b))X | constant |
| SECURE_AUTH_KEY   | IaT>N:]LUq3ghCgI<8Kd!{;CSx<DjOP;S|As5R cJDfDF-<.U}v_{:Tl[!zIxR9k | constant |
| LOGGED_IN_KEY     | %Yu8YeNBZi8 d7Dw|}m6_*?B&I3Cv_Hg]%:d-%7E;J8hmPsHpbTjRH<V_h3BnX-{ | constant |
| NONCE_KEY         | d)6jmy+R^g`- ]4Q8R-CEP:$l-@:4(Y(=(_r9(T4WpFzU!$mTR5&o?q{qw*=ex.t | constant |
| AUTH_SALT         | _?(_kOf5V{a)*YSbb4_E=g]`P[z(Va4/x@xS]M]If &b1oS`+ RsLSy-SuX0r_d? | constant |
| SECURE_AUTH_SALT  | OCsKv6U9koOm*g74V9-Z(cCZMn89?JQOw:NO6N1m1->qV(wg.0G!05d}6zznA}-8 | constant |
| LOGGED_IN_SALT    | oy%3|A9!dWt=q+{+r$s;3*k1&dDO2WN27JO[_TBt,E1Nr* uuf|,7koMBa+#1HE( | constant |
| NONCE_SALT        | y#rfX-<Vz[X!mHwIg(?X]]P$t(#~F#C6f(}&O^?.@9g;7@s_W/|RtDWV^AmR1f*8 | constant |
| WP_CACHE_KEY_SALT | S_xmq*@Xp%p+sw8i.bN**5?*&Otd.|&C#At_h;5H^n,%#9T4.`s785siMz3$@QKb | constant |
+-------------------+------------------------------------------------------------------+----------+
Puede encontrar más información sobre el comando wp config get en la documentación oficial.

### 1.3.4 Paso 4. Instalación de WordPress (wp core install)
Una vez que tenemos la base de datos creada y el archivo de configuración preparado podemos realizar la instalación de WordPress con el comando:

wp core install --url=localhost --title="IAW" --admin_user=admin --admin_password=admin_password --admin_email=test@test.com
En este paso le estamos indicando los siguientes parámetros:

--url=localhost (Dominio del sitio WordPress. En nuestro caso será localhost o la dirección IP del servidor. En una instalación en producción utilizaremos el nombre del dominio del sitio.)
--title="IAW" (Título del sitio WordPress)
--admin_user=admin (Nombre del usuario administrador)
--admin_password=admin_password (Contraseña del usuario administrador)
--admin_email=test@test.com (Email del usuario administrador)
Tenga en cuenta que en su caso tendrá que reemplazar los valores: localhost, IAW, admin, admin_password y test@test.com, por los valores que quiera utilizar para el dominio del sitio, título, nombre, contraseña y dirección de correo del administrador.

Puede encontrar más información sobre el comando wp config install en la documentación oficial.

## 1.4 Comandos útiles
En la documentación oficial puede encontrar un listado de todos los comandos que se puden utilizar.

A continuación, se muestra un pequeño resumen de algunos de los comandos que podemos utilizar con WP-CLI.

### 1.4.1 Actualización de los plugins a la última versión
wp plugin update --all
Puede encontrar más información sobre el comando wp plugin update en la documentación oficial.

### 1.4.2 Actualización de los themes a la última versión
wp theme update --all
Puede encontrar más información sobre el comando wp plugin update en la documentación oficial.

### 1.4.3 Comprobar la versión del core de WordPress
wp core check-update
Puede encontrar más información sobre el comando wp core check-update en la documentación oficial.

### 1.4.4 Actualizar el core de WordPress a la última versión
wp core update
Puede encontrar más información sobre el comando wp core update en la documentación oficial.

### 1.4.5 Cambiar el idioma de WorPress
Podemos listar los idiomas disponibles para WordPress.

wp language core list
Una vez que hemos encontrado el nombre del idioma podemos cambiar el idioma con el siguiente comando.

wp language core install en_US --activate
Puede encontrar más información sobre el comando wp language core en la documentación oficial.

### 1.4.6 Listar los plugins instalados
wp plugin list
Puede encontrar más información sobre el comando wp plugin list en la documentación oficial.

### 1.4.7 Instalar y activar un plugin
Para instalar el plugin bbpress ejecutaríamos el siguiente comando:

wp plugin install bbpress --activate
Puede encontrar más información sobre el comando wp plugin install en la documentación oficial.

### 1.4.8 Desactivar un plugin
Para desactivar el plugin bbpress ejecutaríamos el siguiente comando:

wp plugin deactivate bbpress
Puede encontrar más información sobre el comando wp plugin deactivate en la documentación oficial.

### 1.4.9 Eliminar un plugin
Para eliminar el plugin bbpress ejecutaríamos el siguiente comando:

wp plugin delete bbpress
Puede encontrar más información sobre el comando wp plugin delete en la documentación oficial.

### 1.4.10 Eliminar los plugins que están inactivos
wp plugin delete $(wp plugin list --status=inactive --field=name)
Puede encontrar más información sobre el comando wp plugin delete en la documentación oficial.

### 1.4.11 Listar los themes instalados
wp theme list
Puede encontrar más información sobre el comando wp theme list en la documentación oficial.

### 1.4.12 Instalar y activar un theme
Para instalar el theme sydney ejecutaríamos el siguiente comando:

wp theme install sydney --activate
Puede encontrar más información sobre el comando wp theme install en la documentación oficial.

### 1.4.13 Activar un theme
Para activar el theme twentytwenty ejecutaríamos el siguiente comando:

wp theme activate twentytwenty
Puede encontrar más información sobre el comando wp theme activate en la documentación oficial.

### 1.4.14 Eliminar un theme
Para eliminar el theme sydney ejecutaríamos el siguiente comando:

wp theme delete sydney
Puede encontrar más información sobre el comando wp theme delete en la documentación oficial.

### 1.4.15 Eliminar los themes que están inactivos
wp theme delete $(wp theme list --status=inactive --field=name)
Puede encontrar más información sobre el comando wp theme delete en la documentación oficial.

## 1.5 Entregables
En esta práctica habrá que entregar un documento técnico con la descripción de los pasos que se han llevado a cabo durante todo el proceso.

El documento debe incluir como mínimo lo siguientes contenidos:

URL del repositorio de GitHub donde se ha alojado el documento técnico escrito en Markdown.

Scripts de bash utilizados para realizar el aprovisionamiento de las máquinas virtuales.

Tenga en cuenta que el aprovisionamiento de las máquinas virtuales se realizará mediante un script de bash. Cada máquina usará su propio script. El contenido de cada uno de los scripts deberá ser incluido en el documento y deberá describir qué acciones se han ido realizando en cada uno de ellos.
