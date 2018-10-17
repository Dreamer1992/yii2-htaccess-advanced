# yii2-htaccess-advanced
Example yii2 .htaccess file for advanced application temlate
In root folder .htaccess:

```php
# Mod_Autoindex
<IfModule mod_autoindex.c>
    # Disable Indexes
    Options -Indexes
</IfModule>

# Mod_Rewrite
<IfModule mod_rewrite.c>
    # Enable symlinks
    Options +FollowSymlinks
    # Enable mod_rewrite
    RewriteEngine On

    # Backend redirect
    RewriteCond %{REQUEST_URI} ^/backend
    RewriteRule ^backend(.*) /backend/web/$1 [L]

    # Statics redirect
    RewriteCond %{REQUEST_URI} ^/phpm
    RewriteRule ^phpm/(.*)$ phpm/$1 [L]

    # Frontend redirect
    RewriteCond %{REQUEST_URI} ^(.*)$
    RewriteRule ^(.*)$ frontend/web/$1

    #no end slesh
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_URI} ^(.+)/$
    RewriteRule .* https://%{HTTP_HOST}%1 [R=301,L,QSA]

#Только для сайта на сервере
#    RewriteCond %{HTTPS} off [OR]
#    RewriteCond %{HTTP_HOST} ^www\. [NC]
#    RewriteCond %{HTTP_HOST} ^(?:www\.)?(.+)$ [NC]
#    RewriteCond %{HTTP:X-Forwarded-Proto} !https
#    RewriteRule ^ https://%1%{REQUEST_URI} [L,NE,R=301]
#Только для сайта на сервере

</IfModule>
```
In frontend/web and backend/web .htaccess :

```php


AddDefaultCharset UTF-8
#AddCharset UTF-8 .html
RewriteEngine on

RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d

RewriteRule . index.php
```
