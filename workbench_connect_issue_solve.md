## 1 . Check MariaDB Service Status:
```
sudo systemctl status mariadb
```
## 2. If the service is not running, start it using:
```
sudo systemctl start mariadb
```
## 3. If you made any changes to the configuration, consider restarting the service:
```
sudo systemctl restart mariadb
```
## 4. Verify MariaDB Server Configuration: Check if the MariaDB server is configured to allow remote connections. Open the MariaDB configuration file:
```
sudo nano /etc/my.cnf.d/server.cnf
```
## 5. Look for the bind-address parameter under the [mysqld] section. Ensure it is set to the server's IP address or 0.0.0.0 to listen on all interfaces:
```
[mysqld]
bind-address = 0.0.0.0
```
#### Save the file and restart the MariaDB service:
```
sudo systemctl restart mariadb
```
## 6. Check Firewall Settings: Make sure the necessary ports for MariaDB (default port: 3306) are open on the remote server. CentOS 8 uses firewalld by default. To check the firewall status, run:
```
sudo systemctl status firewalld
```
If it's active, add a rule to allow incoming connections to the MariaDB port:

```
sudo firewall-cmd --add-port=3306/tcp --permanent
sudo firewall-cmd --reload
```
## Check SELinux: If SELinux is enabled on the remote server, it might be blocking the connection. You can temporarily set it to permissive mode to test if SELinux is causing the issue:
```
sudo setenforce 0
```
Try connecting again. If it works now, it means SELinux was the problem. To permanently allow MySQL connections, you need to create a custom SELinux policy or adjust the settings accordingly. Setting SELinux back to enforcing mode after testing:
```
sudo setenforce 1
```
## Check Network Connectivity: Ensure that you have network connectivity to the remote server. Try pinging the server:
```
ping remote_server_ip
```
