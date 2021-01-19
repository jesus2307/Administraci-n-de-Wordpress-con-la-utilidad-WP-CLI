# iaw-practica-09
https://josejuansanchez.org/iaw/practica-wp-cli/index.html


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
