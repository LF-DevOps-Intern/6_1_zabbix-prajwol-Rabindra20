3. Install Latest Zabbix Agent on VM or host machine or server itself to fetch logs, steps include:
- Run as active check agent
- Add a logging item to the same template for fetching /var/log/syslog(Ubuntu) or /var/log/messages
(CentOS)
- Fetch those logs from the host (Make sure required permissions are set for zabbix-agent to
pull logs)
- Provide agent configuration file & screenshots for target machine graph & logs

Steps:<br/>
Install zabbix agent on same vm<br/>
```
Sudo apt install zabbix-agent
```
![install](https://user-images.githubusercontent.com/53372486/144251605-3a00d753-6a90-4c0d-b01a-f5076421fc4f.png)<br/>

Edit zabbix-agent .conf file<br/>
```
sudo nano /etc/zabbix/zabbix_agentd.conf
```
Add below lines in zabbix-agent .conf file<br/>
```
ServerActive=192.168.141.128
Server=192.168.141.128
Hostname=ubuntu
```
![conf](https://user-images.githubusercontent.com/53372486/144251630-cf68ae98-13ec-4a1b-9b35-9f26f4197e4b.png)<br/>

Start zabbix-agent service<br/>
```
systemctl restart zabbix-agent 
```
Check zabbix-agent service<br/>
```
systemctl status zabbix-agent 
```
![status](https://user-images.githubusercontent.com/53372486/144251622-7ab1751b-3bf2-49fb-ac5a-3fec6a9aa068.png)<br/>

Allow 10050 port<br/>
```
sudo ufw allow 10050/tcp
```
On webpage,click on configuration and then click on hosts<br/>
Create host and Template<br/>
![host](https://user-images.githubusercontent.com/53372486/144251636-1ac627bc-a421-4540-ade4-06565c90d17e.png)<br/>

![temp](https://user-images.githubusercontent.com/53372486/144251629-c0cde0a5-c651-4931-abd1-1573082f2134.png)<br/>

Check running host<br/>

![run](https://user-images.githubusercontent.com/53372486/144251618-07e8c066-939d-4839-a04f-21967cafb61e.png)<br/>

Add proxy
click on administration > proxies > create proxy
![proxy active](https://user-images.githubusercontent.com/53372486/144541192-67795f5c-a8c0-4a3a-825f-ffb43fa2adcc.png)<br/>

Give promission to zabbix user<br/>
```
sudo usermod -aG adm zabbix
```
![usermod](https://user-images.githubusercontent.com/53372486/144541210-4cfdc1c8-e21a-4931-8bdd-f0b194e29c7b.png)<br/>

Check zabbix user can access syslog<br/>
```
sudo -H -u zabbix bash -c 'tail -f /var/log/syslog'
```
![checking zabbix](https://user-images.githubusercontent.com/53372486/144541177-b9e3a2a0-a031-45c7-a121-e4d0a6de9abd.png)<br/>

Fetch log<br/>
click on configuration > item > create item<br/>

![log](https://user-images.githubusercontent.com/53372486/144541185-03e1312b-ee30-474f-bf02-5b7e18449839.png)<br/>

![syslogall](https://user-images.githubusercontent.com/53372486/144546424-92246990-a878-4249-82cc-68455d2465e8.png)<br/>

Check log data <br/>
Click on monitring > Latest data > syslog or log (find item name)<br/>

![run](https://user-images.githubusercontent.com/53372486/144251618-07e8c066-939d-4839-a04f-21967cafb61e.png)<br/>

Click on history<br/>
For syslog all data<br/>

![history](https://user-images.githubusercontent.com/53372486/144546457-f152a4f4-3961-458a-a5f0-571943ac7758.png)<br/>

For error and alert log of syslog<br/>

![syslog](https://user-images.githubusercontent.com/53372486/144546447-bb4e89b5-4a96-42c4-a0be-93bf632f8492.png)<br/>

![syslog alert](https://user-images.githubusercontent.com/53372486/144546503-615e1d4d-6b19-49c8-85ab-a9ce3f88fdaa.png)<br/>

Graph<br/>
![graph](https://user-images.githubusercontent.com/53372486/144548213-d41a174a-9db4-422d-bfe1-669a7fcd66e3.png)<br/>

![graph2](https://user-images.githubusercontent.com/53372486/144548214-5572d159-2384-4228-b858-05af32cd1591.png)<br/>

![graph3](https://user-images.githubusercontent.com/53372486/144548216-fb9018f8-b46b-4370-b20f-9c3e71677014.png)<br/>




