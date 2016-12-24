# gce-wordpress
wordpress server deployment log

http://www.linuxserve.com/2015/05/install-latest-wordpress-version-on.html

1. LAMP Server Installation

First of all, we meed to install the LAMP server so that you can run WordPress on Debian. To do this, open the terminal and run these commands:


*sudo apt-get install apache2 mysql-client mysql-server php5 php5-mysql php5-curl php5-gd unzip

During the installation you will be asked to enter a password for the MySQL root user:



Set any password of your choice then proceed.

root/root

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
*$ sudo /etc/init.d/mysql restart

Installing WordPress

Open the terminal and issue these commands:

cd /tmp 
wget -c http://wordpress.org/latest.zip 
sudo apt-get install unzip

sudo unzip -q latest.zip -d /var/www/html/ 

sudo chown -R www-data.www-data /var/www/html/wordpress 

sudo chmod -R 755 /var/www/html/wordpress 

sudo mkdir -p /var/www/html/wordpress/wp-content/uploads 

sudo chown -R www-data.www-data /var/www/html/wordpress/wp-content/uploads


Let's now insert our database details to the WordPress config file. To do this, run these commands:

cd /var/www/html/wordpress/ 
sudo cp wp-config-sample.php wp-config.php

Edit the wp-config.php file with any text editor of your choice. For example, you can use gedit or nano:

sudo gedit wp-config.php

or

sudo nano wp-config.php

Then enter the database name, database user and password you have created earlier:

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'wpdatabase');

/** MySQL database username */
define('DB_USER', 'wpuser');

/** MySQL database password */
define('DB_PASSWORD', 'wppass');

/** MySQL hostname */
define('DB_HOST', 'localhost');

Save your file and exit. Finally open your browser and type this link to complete the installation of WordPress:

http://localhost/wordpress/

Then follow setup instructions:







Posted by Brian Datt
