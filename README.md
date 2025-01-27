
# StudentWebApp Deploy On AWS

##     REQUIREMENTS

1) Web Application           --> Student 
2) Web Application WAR file  --> Student.war
3) DataBase                  --> mysql
4) java open jdk             --> java 1.8.0
5) tomcat (9)                --> apache tomcat 

## Practicle Commands 

### Step 1: Set Up MySql

   search google (mysql download) go to mysql communicaty download > mysql yum repository > copy link address.

   wget (https://dev.mysql.com/get/mysql84-community-release-el9-1.noarch.rpm) 

   ls 

   dnf install mysql84-community-release-el9-1.noarch.rpm 
   
   dnf install mysql-community-server -y                     //here is install mysqlclient 

   systemctl start mysqld
   
   cat /var/log/mysqld.log | grep 'password'             //to show the mysqld password copy password 

   mysql -u root -p(paste password)
 
   select version();

   alter user root@localhost identified by 'Admin@1234'  //To Change this password your mysql
   { AGAIN RUN THIS COMMAND AND PROVIDE THIS NEW PASSWORD} 

   mysql -u root -p
   Enter password: Admin@1234    //(enter the mysql)

   show databases; 

   then --> create database student; 

   show databases; //command QUERY 

   {TO PROVIDE FILE IN (student.sql) COPY DATA ALL PASTE } 

   this data copy & paste 

   use student;     (// RUN QUERY)

            CREATE TABLE if not exists students(student_id INT NOT NULL AUTO_INCREMENT,
	         student_name VARCHAR(100) NOT NULL,
                 student_addr VARCHAR(100) NOT NULL,
	         student_age VARCHAR(3) NOT NULL,
	         student_qual VARCHAR(20) NOT NULL,
	         student_percent VARCHAR(10) NOT NULL,
	         student_year_passed VARCHAR(10) NOT NULL,
	         PRIMARY KEY (student_id)
            );

   // exit 


### Step 2:  Install Apache Tomcat 8 

   wget (https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.98/bin/apache-tomcat-9.0.98.zip) 

   ls

   unzip apache-tomcat-9.0.98.zip


### Step 3:  Install Java (OpenJDK 1.8)

   dnf install java-17-amazon-corretto-devel -y 

   java --version


### Step 4: Change Configuration

   cd apache-tomcat-9.0.98/Conf 

   vim context.xml 

   * (GO LINE NO. 21 and PASTE) 

 vim context.xml

		<Resource name="jdbc/TestDB" auth="Container" type="javax.sql.DataSource"
               maxTotal="100" maxIdle="30" maxWaitMillis="10000"
               username="USERNAME" password="PASSWORD" driverClassName="com.mysql.jdbc.Driver"
               url="jdbc:mysql://DB-ENDPOINT:3306/DATABASE"/>

* (CHANGES THIS FILE ) Username --> root  password --> Admin@1234    DATABASE --> student (change names)  DB-ENDPOINT ---> Instace public ip

 

### Step 5:  copy student.war file in webapps  & copy mysql-coonector.jar file in lib

 - SYNTAX : cp student.war apache-tomcat-9.0.98/webapps 

 - SYNTAX : cp mysql-connector.jar apache-tomcat-9.0.98/lib 

 - SYNTAX : mv mysql-connector.jar apache-tomcat-9.0.98/bin

   cd apache-tomcat-9.0.98/bin 

   ./catalina.sh start     //not start tomcat server then you can give the permission for this service 
   
   chmod 700 catalina.sh

   cd apache-tomcat-9.0.98/bin 

   ./catalina.sh start 


* ADD Port 8080 and 3306 

{HIT IP }

-------->    http://(ip-address):8080/student       <---------

// after you fill the form you can see also backend data , go through mysql databse and hit the query 
 
- SELECT * FROM <table_name>;

you can show your tables list in data.
