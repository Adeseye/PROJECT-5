## IMPLEMENT A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS).


This project I would be demonstrating how a Linux server(client) connects to a Server Linux Database using MySQL Relational Database Management System (RDBMS).

First I'm going to create two Linux-based virtual servers (EC2 instances in AWS)

<code> Server A name - `mysql server`

Server B name - `mysql client`</code>

![alt text](./Images/step%201.JPG)

Install MySQL server on the MySQL Server & MySQL client on the Client Server

Next, both Linux servers has to be on the same local virtual network. This will enable them both to communicate with each other using a local IP addresses.

I will be using MySQL server local IP address to connect from MySQL Client, MySQL server uses TCP port 3306 by default. I will have configure 'Inbound rules' in the security Groups for 'MySQL Server'.

For additional security do not allow all IP address to connect to MySQL Server, only a specific local IP address which will be my 'MySQL client' Linux server.

Which is *172.31.44.68*

![alt text](./Images/Inbound%20security%20group%202.JPG)

I will need to create a Database & a remote user to access database, once I have established a connection between MySQL client and MySQL Server.

I have already installed MySQL, I will need to make it secured. I'm going to run the MySQL secure installation command.

<code>sudo mysql_secure_installation</code>

This will enable to me to set a Password;

Remove anonymous users

Disallow root login remotely

Remove test database

Remove test privileges

This removes default installation settings, that comes preinstalled.

![alt text](./Images/sudo%20msql%20secure%20installation%203.JPG)

Next step is to create a database 

Login to MySQL and run the command

<code>CREATE DATABASE test_db</code>

![alt text](./Images/create%20database%20named%20test%20db%204.JPG)

Create a user to access database

<code>CREATE USER 'remote_user'@' IDENTIFIED WITH mysql_native_password BY 'password';</code>

![alt text](./Images/create%20a%20user%204.JPG)

Next - Is to grant the remote user access to data base(test_db)

<code>GRANT ALL ON test_db.* TO 'remote_user'@'%' WITH GRANT OPTION;</code>

![alt text](./Images/grant%20remote%20user%20to%20data%20base%205.JPG)

Next - Flush privileges

<code>FLUSH PRIVILEDGES</code>

![alt text](./Images/flush%20privileges%205.JPG)

Exit MySQL

![alt text](./Images/exit%20database%206.JPG)

Next step is to configure MySQL Server to allow connections from remote hosts by changing the bind-address from '127.0.0.1' to '0.0.0.0'. 

Run the command to access & edit MySQL database server configuration file.

<code>sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf</code>

![alt text](./Images/configure%20MYSQL%20server%20to%20allow%20connections%20from%20remote%20host%207.JPG)

![alt text](./Images/sudo%20vi%20etc%208.JPG)

Restart MySQL service by running the command

<code>sudo systemctl restart mysql</code>
 
![alt text](./Images/restart%20mysql%209.JPG)

I will attempt to connect to MySQL server Database engine from the MySQL client Linux server, by using mysql utility.

On the MySQL client linux server, run this command:

<code>sudo mysql -u remote_user -h 172.31.43.109 -p</code>

*Command explained*

-u remote_user(This is the user I created)

-h 172.31.43.109(My MySQL Server IP address)

-p(This will prompt for a password to connect)


![alt text](./Images/connecting%20from%20mysql%20client%20to%20mysql%20server%2010.JPG)

Successfully connected to MySQL Server from MySQL client Linux Server using mysql utility.

Now I'm going to run SQL query command

<code>Show database ;</code>

![alt text](./Images/show%20database%2011.JPG)

I have successfully deployed a fully functioning MySQL Client to Server setup.

END...








