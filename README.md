# PDO_IBM-1.3.4-patched
PHP 7.0 pdo_ibm extension patched to resolve a segmentation fault error.

This patch resolves the bug posted here https://bugs.php.net/bug.php?id=72424
    
This patch is taken from this post https://bugs.php.net/bug.php?id=72121

## Installing IBM DB2 Driver.

Head to https://www-01.ibm.com/marketing/iwm/iwm/web/preLogin.do?source=swg-idsdpds and download the right version of IBM Data Server Driver Package for your OS. (Requires opening a free account).

0. Extract the downloaded package at ~/dsdriver
1. cd ~/dsdriver
2. sudo chmod +x installDSDriver
3. sudo apt-get install ksh
4. sudo ksh installDSDriver

Currently the include path needs a little help finding things...
  
5. sudo ln -s /home/username/dsdriver/include /include

Clone, compile and make the driver

6. cd ~/
7. git clone https://github.com/dreamfactorysoftware/PDO_IBM-1.3.4-patched.git
8. cd ~/PDO_IBM-1.3.4-patched
9. phpize
10. ./configure --with-pdo-ibm=/home/username/dsdriver/lib
11. make
12. make test (optional)
13. sudo make install

Make the driver easy to enable (Ubuntu)

16. echo "extension=pdo_ibm.so" | sudo tee /etc/php/7.0/mods-available/pdo_ibm.ini
17. sudo phpenmod pdo_ibm
18. sudo service php7.0-fpm restart

Verify that the pdo_ibm extension is loaded
19. php -m | grep ibm
20. Use phpinfo() to check for pdo_ibm on web server setup (apache2 or nginx).
