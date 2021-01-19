# 1 Práctica: Administración de Wordpress con la utilidad WP-CLI
En esta práctica vamos a realizar la administración de un sitio WordPress desde el terminal con la utilidad WP-CLI.

Con la utilidad WP-CLI podemos realizar las mismas tareas que se pueden hacer desde el panel de administración web de WordPress, pero desde la línea de comandos.

En la web oficial de WordPress podemos encontrar:

el manual de uso de WP-CLI
los comandos de WP-CLI.
## 1.1 Requisitos
La máquina donde vamos a instalar la utilidad WP-CLI será la misma máquina donde queremos realizar la instalación de WordPress y tendrá que tener instalado todo el software necesario de la pila LAMP.

## 1.2 Instalación de WP-CLI en el servidor LAMP
Descargamos el archivo wp-cli.phar del repositorio oficial de WP-CLI. Los archivos .phar son unos archivos similares a los archivos .jar de Java. Estos archivos se utilizan para distribuir aplicaciones o librerías de PHP en un único archivo. Puede encontrar más información sobre los archivos .phar en la documentación oficial de PHP.

## 1.3 Ejemplo de uso: Instalación de WordPress con WP-CLI
Vamos a realizar un ejemplo de uso sobre una máquina que ya tiene instalado todo el software necesario de la pila LAMP.

### 1.3.1 Paso 1. Descarga del código fuente de WordPress (wp core download)
### 1.3.2 Paso 2. Creación del archivo de configuración (wp config create)
### 1.3.3 Paso 3. Comprobación de los valores del archivo de configuración (wp config get)
### 1.3.4 Paso 4. Instalación de WordPress (wp core install)

## 1.4 Comandos útiles
En la documentación oficial puede encontrar un listado de todos los comandos que se puden utilizar.

A continuación, se muestra un pequeño resumen de algunos de los comandos que podemos utilizar con WP-CLI.

### 1.4.1 Actualización de los plugins a la última versión
### 1.4.2 Actualización de los themes a la última versión
### 1.4.3 Comprobar la versión del core de WordPress
### 1.4.4 Actualizar el core de WordPress a la última versión
### 1.4.5 Cambiar el idioma de WorPress
1.4.6 Listar los plugins instalados
wp plugin list
Puede encontrar más información sobre el comando wp plugin list en la documentación oficial.

1.4.7 Instalar y activar un plugin
Para instalar el plugin bbpress ejecutaríamos el siguiente comando:

wp plugin install bbpress --activate
Puede encontrar más información sobre el comando wp plugin install en la documentación oficial.

1.4.8 Desactivar un plugin
Para desactivar el plugin bbpress ejecutaríamos el siguiente comando:

wp plugin deactivate bbpress
Puede encontrar más información sobre el comando wp plugin deactivate en la documentación oficial.

1.4.9 Eliminar un plugin
Para eliminar el plugin bbpress ejecutaríamos el siguiente comando:

wp plugin delete bbpress
Puede encontrar más información sobre el comando wp plugin delete en la documentación oficial.

1.4.10 Eliminar los plugins que están inactivos
wp plugin delete $(wp plugin list --status=inactive --field=name)
Puede encontrar más información sobre el comando wp plugin delete en la documentación oficial.

1.4.11 Listar los themes instalados
wp theme list
Puede encontrar más información sobre el comando wp theme list en la documentación oficial.

1.4.12 Instalar y activar un theme
Para instalar el theme sydney ejecutaríamos el siguiente comando:

wp theme install sydney --activate
Puede encontrar más información sobre el comando wp theme install en la documentación oficial.

1.4.13 Activar un theme
Para activar el theme twentytwenty ejecutaríamos el siguiente comando:

wp theme activate twentytwenty
Puede encontrar más información sobre el comando wp theme activate en la documentación oficial.

1.4.14 Eliminar un theme
Para eliminar el theme sydney ejecutaríamos el siguiente comando:

wp theme delete sydney
Puede encontrar más información sobre el comando wp theme delete en la documentación oficial.

1.4.15 Eliminar los themes que están inactivos
wp theme delete $(wp theme list --status=inactive --field=name)
Puede encontrar más información sobre el comando wp theme delete en la documentación oficial.

1.5 Entregables
En esta práctica habrá que entregar un documento técnico con la descripción de los pasos que se han llevado a cabo durante todo el proceso.

El documento debe incluir como mínimo lo siguientes contenidos:

URL del repositorio de GitHub donde se ha alojado el documento técnico escrito en Markdown.

Scripts de bash utilizados para realizar el aprovisionamiento de las máquinas virtuales.

Tenga en cuenta que el aprovisionamiento de las máquinas virtuales se realizará mediante un script de bash. Cada máquina usará su propio script. El contenido de cada uno de los scripts deberá ser incluido en el documento y deberá describir qué acciones se han ido realizando en cada uno de ellos.

















#### Vamos al directorio de Apache
cd /var/www/html

#### Descargamos el contenido
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar

#### Le damos permisos
chmod +x wp-cli.phar

#### cmbiamos la ubicacion 
mv wp-cli.phar /usr/local/bin/wp

#### Eliminamos el index
rm -rf index.html

#### descargamos worpress en español y le damos permiso de root
wp core download --path=/var/www/html --locale=es_ES --allow-root

#### Asignamos permisos
chown -R www-data:www-data /var/www/html

#### creamos el archivo de configuracion
wp config create --dbname=$DB_NAME --dbuser=$DB_USER --dbpass=$DB_PASSWORD --allow-root

#### instalamos worpress
wp core install --url=$IP --title="jesus" --admin_user=jesus --admin_password=jesus --admin_email=jesus@gmail.com --allow-root
