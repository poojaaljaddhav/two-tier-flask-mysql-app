
#Below command will show existing docker network
docker network ls 

#Create Network in docker to run your two tier app
docker network create

#create MYSQL Container of docker using docker network
docker run -d -v $(pwd):/var/lib/mysql --network twotier --name two-tier-mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=test@123 -e MYSQL_DB=KYC mysql:5.7

#Create flash app container
docker run -d -p 5000:5000 --network twotier -e MYSQL_HOST=two-tier-mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=test@123 -e MYSQL_DB=KYC two-tier-backend:latest

#some useful docker commands
docker login
docker images
docker push poojaaljaddhav/batch-6-pyhon

#—will help to delete images not associated with container
docker system prune 

#—will help to delete images
docker rmi (image_id) —force 

#below command help to change name of docker images 
docker tag batch-6-python:latest poojaaljaddhav/batch-6-pyhon:latest

#Network 

docker nework ls
docker network ls
docker network create twotier
docker network ls


#LOGIN INSIDE MYSQL DB

ubuntu@ip-172-31-26-42:~/docker_projects/DB/data$ docker exec -it 59bba6534caa bash
bash-4.2# mysql -u
mysql: [ERROR] mysql: option '-u' requires an argument
bash-4.2# ysql -u root -p
bash: ysql: command not found
bash-4.2# mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.7.44 MySQL Community Server (GPL)

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases
    -> 
    -> 
    -> 
    -> 
    -> ;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.00 sec)

mysql> 
mysql> create database KYC
    -> ;
Query OK, 1 row affected (0.00 sec)

mysql> use database KYC
ERROR 1049 (42000): Unknown database 'database'
mysql> use KYC
Database changed
mysql> create TABLE messages (id INT AUTO_INCREMENT PRIMARY KEY, message TEXT);
Query OK, 0 rows affected (0.03 sec)

mysql> insert into messages (message) values ("KYC for user 1")
    -> ;
Query OK, 1 row affected (0.02 sec)

mysql> insert into messages (message) values ("KYC for user 2");
Query OK, 1 row affected (0.00 sec)

mysql> insert into messages (message) values ("KYC for user 3");
Query OK, 1 row affected (0.00 sec)

mysql> select * from messages;
+----+----------------+
| id | message        |
+----+----------------+
|  1 | KYC for user 1 |
|  2 | KYC for user 2 |
|  3 | KYC for user 3 |
+----+----------------+
3 rows in set (0.00 sec)

mysql> exit

