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
    mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;
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

Troubleshoot
-------------

    $ sudo systemctl status mysql.service
    $ sudo systemctl restart mysql.service

Datbase Information
-------------------

    $ mysql -u username -p
    mysql> select distinct table_schema from information_schema.tables;



References
----------

    https://dev.mysql.com/doc/mysql-getting-started/en/
    https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/
    https://www.tutorialspoint.com/mysql-secure-installation-improve-mysql-installation-security
    https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04
