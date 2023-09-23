# Persist-data-between-two-MySQL-database-hosted-on-two-different-Ec2-instances-using-EBS
What we are going to make:

<img width="740" alt="what-we-going-to-make" src="https://github.com/nobelrakib/Persist-data-between-two-MySQL-database-hosted-on-two-different-Ec2-instances-using-EBS/assets/53372696/eb103345-84ba-4d9d-bbca-e654249512df">

At first launch two ec2 instances and attach a 20 GB EBS volume on instance1.

<img width="762" alt="vmlist" src="https://github.com/nobelrakib/Persist-data-between-two-MySQL-database-hosted-on-two-different-Ec2-instances-using-EBS/assets/53372696/055976a4-2755-4aaa-b73d-c5ef3e8117dc">


<img width="605" alt="20-gb-ebs-volumn" src="https://github.com/nobelrakib/Persist-data-between-two-MySQL-database-hosted-on-two-different-Ec2-instances-using-EBS/assets/53372696/4111037b-5a87-4842-ad90-72b689c83baf">

Now check in instance one list of block using lsblk

<img width="308" alt="vm1listofblock" src="https://github.com/nobelrakib/Persist-data-between-two-MySQL-database-hosted-on-two-different-Ec2-instances-using-EBS/assets/53372696/db1988a5-bd60-4f5c-8b42-84a0d6a53311">

See a twenty GB storage has been attached named xvdb.

Now there is no file system in this block storage.

Make a file system.

<img width="505" alt="vm1makefilesystem" src="https://github.com/nobelrakib/Persist-data-between-two-MySQL-database-hosted-on-two-different-Ec2-instances-using-EBS/assets/53372696/ac93e438-a06a-4dfb-a205-4c823ee648d3">

Now create a folder named mydata and mount it with our block storage.

```
mount /dev/xvdb /home/ubuntu/mydata/
```
Now install docker and run a MySQL container.

```
1.sudo apt install docker.io docker-compose
#create a compose file named docker-compose.yaml
version: "3"

services:
  mysql:
    image: mysql:latest
    container_name: db
    environment:
      MYSQL_ROOT_PASSWORD: a
      MYSQL_DATABASE: db
      MYSQL_USER: a
      MYSQL_PASSWORD: a
    volumes:
      - ./mydata:/var/lib/mysql
    ports:
      - "3306:3306"
    restart: always
#run this command to run the MySQL container
2.sudo docker-compose up
```
<img width="960" alt="vm1dockercontainer" src="https://github.com/nobelrakib/Persist-data-between-two-MySQL-database-hosted-on-two-different-Ec2-instances-using-EBS/assets/53372696/8dcfe7d0-d56a-4e5e-994c-18af7b5eb050">

Now go inside the the MySQL container and insert some data which will be saved in our EBS. In our compose file we have added volume for which our all MySQL data will be stored in our mydata folder and mydata folder is mounted with our EBS.

```
#Go inside mysql container
1.docker exec -it db bash
#give user name and password of MySQL
2.mysql -u root -p
3.use db;
4.CREATE TABLE person (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    age INT
);
5.INSERT INTO person (name, age) VALUES
('John Doe', 30),
('Jane Smith', 25),
('Bob Johnson', 40),
('Alice Brown', 35),
('Eva Davis', 28);
```
<img width="302" alt="vm1mysqldatainsert" src="https://github.com/nobelrakib/Persist-data-between-two-MySQL-database-hosted-on-two-different-Ec2-instances-using-EBS/assets/53372696/992e6edd-539f-45b0-84bd-d185257b897a">

Now detach the EBS volume from instance one and attach it at instance two.










