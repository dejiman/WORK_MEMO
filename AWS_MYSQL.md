# work flow from AWS instance to mysql grant ip 
1.aws login 
 id/passwd  copy&paste not work 
2.top> service >computing EC2  'select'  
3.left menu> instance 'select'
4-1. work> instance status >reboot (restart linux )
4-2. work > link 
1.using puttygen ,convert private keypair file from '*.pem'  to '*.ppk'
2.'run' putty ,insert (ec2-user@public DNS)  to host textinput area  
3. connection menu 'select' -> Seconds between keepalives  => 180 (sec) 
4.private key file for authentication > select '*.ppk' which has been created  with puttygen, select 'Open' button 
5. connect server successfuly , connect to mysql with root user
6. use sudo and select database
 
 sudo su
 show databases; -- check list of databases 
 use 'database name'; -- select database
 show tables;       -- check tables 
 
 
insert user/passwd and grant for all IP 
INSERT INTO mysql.user (host,user,password) VALUES ('%','USERID',password('password')); --- 
GRANT ALL PRIVILEGES ON *.* TO 'userid'@'%';
FLUSH PRIVILEGES; --- apply chanes to databases

limit to some specific IP
INSERT INTO mysql.user (host,user,password) VALUES ('111.222.%','root',password('password'));
GRANT ALL PRIVILEGES ON *.* TO 'root'@'111.222.%';
FLUSH PRIVILEGES;

only one specific IP
INSERT INTO mysql.user (host,user,password) VALUES ('111.222.33.44','root',password('password'));
GRANT ALL PRIVILEGES ON *.* TO 'root'@'111.222.33.44';
FLUSH PRIVILEGES;

recorver

DELETE FROM mysql.user WHERE Host='%' AND User='root';
FLUSH PRIVILEGES; 

