## IMPLEMENT A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS).


This project I would be demonstrating how a Linux server(client) connects to a Linux Database (Server) using MySQL Relational Database Management System (RDBMS).

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




