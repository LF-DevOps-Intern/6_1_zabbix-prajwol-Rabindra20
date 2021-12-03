1. Install Zabbix Server 5 on VM that includes:
- Zabbix Server
- Database
- Apache
- PHP
- Zabbix Server-Modules for Apache & Database
- Zabbix Fronted

Steps:<br/>
Installing the Zabbix Server<br/>
Download and install the repository configuration package<br/>
```
wget https://repo.zabbix.com/zabbix/5.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_5.4-1+ubuntu20.04_all.deb
```
![zabbix](https://user-images.githubusercontent.com/53372486/144222935-e6ec97bc-317c-461a-a83f-118658f898ec.png)<br/>
```
dpkg -i zabbix-release_5.4-1+ubuntu20.04_all.deb
```
![dpkg](https://user-images.githubusercontent.com/53372486/144222917-9a61f09a-0023-4492-9abc-94759613283c.png)<br/>

Update the package<br/>
```
sudo apt update 
```
install the Zabbix server and web frontend with MySQL database support<br/>
```
Sudo apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts
```
![install](https://user-images.githubusercontent.com/53372486/144222924-6680a84f-54e9-45f6-b174-5ee6589de3e6.png)<br/>

Configuring the MySQL Database for Zabbix<br/>
Log into MySQL as the root user using the root password that you set up during the MySQL server installation<br/>
```
mysql -uroot -p
```
![mysql](https://user-images.githubusercontent.com/53372486/144222927-7b7f1e79-e7da-4f76-b1bc-ef63091f6e78.png)<br/>

Create the Zabbix database with UTF-8 character support<br/>
```
create database zabbix character set utf8 collate utf8_bin;
```
create a user that the Zabbix server<br/>
```
create user zabbix@localhost identified by 'Rabindra@1';
```
give it access to the new database, and set the password for the user<br/>
```
grant all privileges on zabbix.* to zabbix@localhost;
```
Exit out of the database console<br/>
```
quit; 
```
![addmysql](https://user-images.githubusercontent.com/53372486/144222907-b65d1758-594e-41c5-86ad-84c1b94a2025.png)<br/>

Run the following command to set up the schema and import the data into the zabbix database. Use zcat since the data in the file is compressed.<br/>
```
zcat /usr/share/doc/zabbix-server-mysql/create.sql.gz | mysql -uzabbix -p zabbix
```
![connectmysql](https://user-images.githubusercontent.com/53372486/144222913-f1b0fa29-36d6-44d1-97ee-980660db2c7b.png)<br/>

Edit file zabbix_server.conf<br/>
```
sudo nano /etc/zabbix/zabbix_server.conf
```
Add below line zabbix_server.conf<br/>
```
DBPassword=Rabindra@1
```
Restart zabbix-server apache2<br/>
```
systemctl restart zabbix-server  apache2
```
Check status<br/>
```
systemctl status zabbix-server zabbix-agent apache2
```
![status](https://user-images.githubusercontent.com/53372486/144222930-3e69e05f-0ae5-4e28-88f0-9db5d8565153.png)






