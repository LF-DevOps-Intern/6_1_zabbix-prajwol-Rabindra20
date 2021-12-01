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




