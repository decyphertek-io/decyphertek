MySQL
=====

MySQL is an open source Database used by enterprsies globally. 

Install
-------

    $ sudo apt update
    $ sudo apt install mysql-server
    $ sudo systemctl start mysql.service
    $ sudo mysql
    mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
    mysql> exit
    $ sudo mysql -u root -p
    # CAUTION!!!! The auth_socket Commands breaks things. 
    mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;
    mysql> exit
    $ sudo mysql_secure_installation

Create a Dedicated User
-----------------------

    $ sudo mysql
    $ mysql -u root -p
    mysql> CREATE USER 'username'@'host' IDENTIFIED WITH authentication_plugin BY 'password';
    mysql> CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
    mysql> CREATE USER 'username'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
    mysql> GRANT PRIVILEGE ON database.table TO 'username'@'host';
    # Limted Permissions
    mysql> GRANT CREATE, ALTER, DROP, INSERT, UPDATE, DELETE, SELECT, REFERENCES, RELOAD on *.* TO 'username'@'localhost' WITH GRANT OPTION;
    <OR>
    # Root level permissions
    mysql> GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' WITH GRANT OPTION;
    mysql> FLUSH PRIVILEGES;
    mysql> exit
    # login to test new account
    $ mysql -u username -p

Change User Password
--------------------

    # Login to root and change Username password
    $ mysql -u root -p
    mysql> ALTER USER 'username'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
    mysql> FLUSH PRIVILEGES;
    mysql>exit
    # Verify
    $ mysql -u username -p
    mysql> exit

Mysql Queries
-------------

    mysql> USE my_table;
    mysql> SELECT * FROM my_table WHERE product = 'Electronics';
    mysql> SELECT * FROM my_table WHERE product = 'Electronics' AND price < 100;
    mysql> SELECT * FROM my_table WHERE price < 100;
    mysql> SELECT * FROM my_table WHERE rrice <= 0 OR price > 100; 

Troubleshoot
-------------

    $ sudo systemctl status mysql.service
    $ sudo systemctl restart mysql.service

Datbase Information
-------------------

    $ mysql -u username -p
    mysql> select distinct table_schema from information_schema.tables;

MariaDB
-------

    # If setting root password
    $ sudo mysql
    $ use mysql;
    # mysql commands should work now on MariaDB
    Mysql> ALTER USER 'user'@'localhost' IDENTIFIED BY 'new_password';
    MySql> FLUSH PRIVILEGES;
    MySql> exit
    # Create a new user
    $ mariadb -u root -p
    $ use mysql;
    $ CREATE USER username@t127.0.0.1 IDENTIFIED BY 'new_passwrod';

Manage Database
---------------

     * debeaver-ce
     * CloudBeaver
     * Beekeper Studio
     * myPHPadmin
     * pgAdmin
     * mysql editor


References
----------

    https://dev.mysql.com/doc/mysql-getting-started/en/
    https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/
    https://linuxconfig.org/how-to-change-mariadb-user-password
    https://www.tutorialspoint.com/mysql-secure-installation-improve-mysql-installation-security
    https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04
