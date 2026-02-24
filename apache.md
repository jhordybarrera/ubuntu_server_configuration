
# Instalar apache
```
sudo apt install apache2 -y
```

# Habilitar PHP-FPM Apache
```
sudo a2enmod proxy_fcgi setenvif && sudo a2enconf php-fpm
```
# Permisos de carpeta apache 

> (Se recomienda que solo el usuario tenga acceso de edición a los ficheros de configuración)
```
sudo chown -R $USER /var/www/html/
```

# Configurar apache

**Habilitar el modulo header apache**
```
sudo a2enmod headers
```
# Probar Configuración Apache
```
apachectl configtest
```

# Habilitar modulo rewrite
```
sudo a2enmod rewrite
```
# reiniciar servicio apache
```
sudo systemctl restart apache2
```

# Habilitar modulo ssl
```
sudo a2enmod ssl
```
# Recargar configuración de apache
```
sudo systemctl reload apache2
```

# Host Virtuales Apache
```
sudo nano /etc/apache2/sites-available/000-default.conf
```

**Editar archivo de configuración**
```
sudo nano /etc/apache2/apache2.conf
```

**Caché para tipos de archivo**
```
<FilesMatch ".(js|css|jpg|jpeg|png|gif|ico|swf|mp4|webm|svg)$">
    Header set Cache-Control "max-age=31536000, public"
    Header unset Last-Modified
    Header unset ETag
</FilesMatch>
```

**Sobreescribir rutas url (pretty urls)**
```
<Directory /var/www/>
        AllowOverride All
</Directory>
```

**Usar versión específica de php fpm**
```
<FilesMatch "\.php$">
    SetHandler "proxy:unix:/run/php/php8.1-fpm.sock|fcgi://localhost/"
</FilesMatch>
```
