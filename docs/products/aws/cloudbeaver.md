Cloudbeaver is an open-source database management tool designed for web-based use, allowing users to manage and query databases through a user-friendly interface. It supports various database types, enabling seamless access and interaction with data across different platforms. With features like SQL editor, data visualization, and user management, Cloudbeaver simplifies database tasks for developers and data analysts alike. [AWS Marketplace: CloudBeaver ](https://aws.amazon.com/marketplace/pp/prodview-5q3uokjkbyuy4?sr=0-4&ref_=beagle&applicationId=AWSMPContessa)


Note:
-----
* Please be aware that it takes a few minutes for the system to be up and running.
* The best way to check is to view the status check from the ec2 / instances / dashboard.
* If it says intializing, it is not ready yet.

SSH Into the server:
--------------------
* Linux + MAC - add .pem key to 
```
vim ~/.ssh/id_rsa
# change permisisons 
chmod 400 id_rsa
```
* ssh core@ip-of-server
* If using putty or mobaxterm make sure to convert .pem using puttygen.

Passwords: DB AND/OR User:
-------------------------
* ssh into server
```
cat ~/.docker/.env
```
* This will display the randomly generated passwords for DB AND/OR User.

Cloudbeaver Setup:
-------------------
* https://ip-of-server
* Welcome screen > click next
* Server Configuration > Set your admin credentials > click next
* Finish setup  > Login with your new credentials
* Gear icon > Back to app
* Connect the Database > Plus Icon > New Connection > PostgresSQl
* Get Postgres DB Password > ssh into server > cat .docker/.env > copy password after = > Return to Cloudbeaver GUI
* Postgres settings : HOST=172.19.0.7 , Database=cloudbeaver, ConnectionName=PostgreSQL@172.19.0.7, UserName=cloudbeaver , Password= ,save credentails > Create
* Note: You can connect any database that is accessible via cloudbeaver.
```
PostgresSQL - Create Test Data
docker exec -it postgres psql -U cloudbeaver -d cloudbeaver
CREATE TABLE test_table(id SERIAL PRIMARY KEY, name VARCHAR(50));
INSERT INTO test_table(name) VALUES ('adminotaur'), ('decyphertek');
SELECT * FROM test_table;
```

Portainer - Manage Docker:
-------------------------
* How to access Portainer to manage your containers > https://ip-of-server:9443
* Follow the instructions to create a new admin account.
* Caution - Portainer can timeout if you dont create an account fast enough
* If this happens you need to restart the container, ssh into the server, then run:
```
docker restart portainer
```
* Once logged into portainer, click get started and select local. You can manage docker from here.

Manage Flatcar Linux:
--------------------
* Optional: Manaully update Flatcar. Updates will happen automatically.
* If you want to manually check for updates run this command: 
```
update_engine_client -update
```

References:
-----------
* https://docs.docker.com/
* https://docs.portainer.io/
* https://www.flatcar.org/docs/latest
* https://dbeaver.com/docs/cloudbeaver/