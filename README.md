# ionCube on Ubuntu 14.04.x


download and extract the IonCube Loader PHP modules
```
cd /var/www/html
wget http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz
tar xvfz ioncube_loaders_lin_x86-64.tar.gz
cd ioncube
```

navigate over to server IP address + /ioncube/loader-wizard.php
```
e.g http://10.1.1.123/ioncube/loader-wizard.php
Select Local install
```

*Loader Wizard* will suggests which module to use
```
e.g ioncube_loader_lin_5.5.so
```

run the following command in terminal to find php extension_dir,
```
php -i | grep extension_dir
```

copy extension_dir path for next step
```
/usr/lib/php5/20121212
```

move module to php extension_dir
```
mv ioncube_loader_lin_5.5.so /usr/lib/php5/20121212
```

create ioncube.ini in Ubuntu 14.04
```
echo "zend_extension = /usr/lib/php5/20121212/ioncube_loader_lin_5.5.so" | sudo tee /etc/php5/mods-available/ioncube.ini
```

soft link to apache2
```
cd /etc/php5/apache2/conf.d 
sudo ln -fs /etc/php5/mods-available/ioncube.ini 01-ioncube.ini
```

soft link to cli
```
cd /etc/php5/cli/conf.d 
sudo ln -fs /etc/php5/mods-available/ioncube.ini 01-ioncube.ini
```
restart Apache2 for module to be loaded
```
service apache2 restart
```

refresh the webpage "http://10.1.1.123/ioncube/loader-wizard.php" to verify that the loader installed
