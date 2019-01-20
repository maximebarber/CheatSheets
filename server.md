# Server

## 1. Connect to public server
> ssh root@server.ip

## 2. Modify rights
> chown -R www-data FILE_NAME

## 3. Modify routes

* Go to etc/apache2/sites-available
* Modify DocumentRoot and Directory
* Delete symlink in sites-enabled
* Enable virtual host files
> a2ensite test.com.conf
> service apache2 reload
