# gce-wordpress
wordpress server deployment log

http://www.linuxserve.com/2015/05/install-latest-wordpress-version-on.html

1. LAMP Server Installation

First of all, we meed to install the LAMP server so that you can run WordPress on Debian. To do this, open the terminal and run these commands:

su - 
apt-get install apache2 mysql-client mysql-server php5 php5-mysql php5-curl php5-gd

During the installation you will be asked to enter a password for the MySQL root user:



Set any password of your choice then proceed.

2. Creating WordPress Database

Let's now create a database for WordPress. From the terminal, write this (use the MySQL password set earlier):

mysql -u root -p

Now run this sequence of commands to create the database, database user & password:

CREATE DATABASE wpdatabase; 
CREATE USER wpuser@localhost IDENTIFIED BY 'wppass'; 
GRANT ALL PRIVILEGES ON wpdatabase.* TO wpuser@localhost; 
FLUSH PRIVILEGES; 
exit

Restart now Apache and MySQL servers with these commands so that changes are taken into effect:

service apache2 restart 
service mysql restart

*$ sudo /etc/init.d/apache2 restart

Installing WordPress

Open the terminal and issue these commands:

cd /tmp 
wget -c http://wordpress.org/latest.zip 
unzip -q latest.zip -d /var/www/html/ 
chown -R www-data.www-data /var/www/html/wordpress 
chmod -R 755 /var/www/html/wordpress 
mkdir -p /var/www/html/wordpress/wp-content/uploads 
chown -R www-data.www-data /var/www/html/wordpress/wp-content/uploads

Let's now insert our database details to the WordPress config file. To do this, run these commands:

cd /var/www/html/wordpress/ 
cp wp-config-sample.php wp-config.php

Edit the wp-config.php file with any text editor of your choice. For example, you can use gedit or nano:

gedit wp-config.php

or

nano wp-config.php

Then enter the database name, database user and password you have created earlier:



Save your file and exit. Finally open your browser and type this link to complete the installation of WordPress:

http://localhost/wordpress/

Then follow setup instructions:







Posted by Brian Datt
