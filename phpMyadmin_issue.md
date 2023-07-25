## Enable the Remi repository:
```
sudo dnf install dnf-utils
sudo dnf install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
```

## Install phpMyAdmin:
```
sudo dnf --enablerepo=remi install phpMyAdmin
```

## File Permissions:
```
sudo chown -R apache:apache /path/to/phpmyadmin
sudo chmod -R 755 /path/to/phpmyadmin
```

## Apache Configuration:
```
<Directory /usr/share/phpMyAdmin/>
   Options Indexes FollowSymLinks
   AllowOverride None
   Require all granted
</Directory>
```

## SELinux Settings:
```
sudo setenforce 0
```

##  Firewall Settings:
```
sudo firewall-cmd --list-all
```

## If HTTP is not listed as allowed, you can open it with the command:
```
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload
```

## Restart Apache:
```
sudo systemctl restart httpd
```
