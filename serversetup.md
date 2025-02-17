# Github

https://github.com/speedcubing-top

# Web Things

Main Site: https://speedcubing.top  
HTTP API: https://api.speedcubing.top  
phpMyAdmin: https://db.speedcubing.top  
Code-Server: https://editor.speedcubing.top  
Jenkins: https://jenkins.speedcubing.top  
Minecraft Panel: https://panel.speedcubing.top  

# Files
Everything is in /home/andy/speedcubing/
- build/ Jar Builds
- cert/ SSL Certificate for Nginx
- dbbackup/ MariaDB Backup
- filehost/ https://speedcubing.top/filehost
- HTTPAPI/ HTTP API
- java/ Java Runtime Environment
- notes/ https://speedcubing.top/notes
- Permanent/ 24/7 Java Process
- website/ Main Site

# Applications

## Nginx
```25080``` (HTTPS, SSL) 
- speedcubing.top, www.speedcubing.top -> ```20081```
- api.speedcubing.top -> ```20082```
- phpmyadmin -> ```1234```

## Express Servers
```20081``` https://speedcubing.top (Express Server + React)  
```20082``` https://api.speedcubing.top (Express Server) 

## 24/7 Java Process
```25000``` (https://github.com/speedcubing-top/Permanent)
## Caddy
```6969``` -> pterodactyl (https://panel.speedcubing.top)
## Code-Server
```1235``` (https://editor.speedcubing.top)
## Jenkins
```1236```
## MariaDB
```3306```
## phpMyAdmin
```1234``` (https://db.speedcubing.top)
## SSH/SFTP
```22```

## Tailscale

## Cloudflared
phpMyAdmin: https://db.speedcubing.top  
Code-Server: https://editor.speedcubing.top  
Jenkins: https://jenkins.speedcubing.top  
Minecraft Panel: https://panel.speedcubing.top  

# Minecraft Servers
```25565``` Internal Proxy  
```25567``` Public Proxy  
```25558``` Public Proxy 2  
```25570``` Lobby  
```25571``` Reduce  
```25572``` MLGRush  
```25573``` Practice  
```25574``` FastBuilder  
```25575``` KnockBackFFA  
```25576``` Clutch  
```25577``` Limbo  
```25578``` Bedwars  
```25579``` Building  

## Plugins

speedcubingLib

speedcubingCommon
- depends: speedcubingLib

speedcubingProxy
- depends: speedcubingLib
- shade: speedcubingCommon

speedcubingServer
- depends: speedcubingLib
- shade: speedcubingCommon

GamePlugin (ex: Lobby, Reduce, Practice, FastBuilder, Limbo...)
- depends: speedcubingLib
- depends: speedcubingServer

## Proxy Server (VelocityPowered)
plugins:
- speedcubingLib
- speedcubingProxy

## Spigot Server (CubingPaper)
plugins:
- speedcubingLib
- speedcubingServer
- GamePlugin

# Installation Script

```shell
apt install sudo
apt install curl
apt install nano
apt install gnupg
apt install screen
apt install ufw
apt install php-fpm
apt install maven
apt install htop
apt install iotop

# npm
apt install npm
npm config set fund false --location=global

# nginx
apt install nginx
rm /etc/nginx/sites-enabled/default
systemctl restart nginx
 
# mysql (install deb first)
dpkg -i mysql-apt-config_0.8.32-1_all.deb
apt update
apt install mysql-server

# phpmyadmin
apt install phpmyadmin
apt remove apache2
apt purge apache2
apt autoremove
```

# Network Interface

### config 
/etc/network/interfaces
```cfg
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
allow-hotplug eth0
iface eth0 inet static
address 192.168.1.96
netmask 255.255.255.0
gateway 192.168.1.1
```

### script
```
systemctl restart networking
```

# Application Configuration/Scripts

## Caddy

### config
/etc/caddy/Caddyfile
```cfg
{
   servers :6969 {
        timeouts {
            read_body 120s
        }
    }
}

# Replace the example <domain> with your domain name or IP address
:6969 {
    root * /var/www/pterodactyl/public

    file_server

    php_fastcgi unix//run/php/php8.3-fpm.sock {
        root /var/www/pterodactyl/public
        index index.php

        env PHP_VALUE "upload_max_filesize = 100M
        post_max_size = 100M"
        env HTTP_PROXY ""
        # env HTTPS "on" # IMPORTANT: this is commented out, to disable HTTPS

        read_timeout 300s
        dial_timeout 300s
        write_timeout 300s
    }

    header Strict-Transport-Security "max-age=16768000; preload;"
    header X-Content-Type-Options "nosniff"
    header X-XSS-Protection "1; mode=block;"
    header X-Robots-Tag "none"
    header Content-Security-Policy "frame-ancestors 'self'"
    header X-Frame-Options "DENY"
    header Referrer-Policy "same-origin"

    request_body {
        max_size 100m
    }

    respond /.ht* 403

    log {
        output file /var/log/caddy/pterodactyl.log {
            roll_size 100MiB
            roll_keep_for 7d
        }
        level INFO
    }
}
```

## code-server

https://github.com/coder/code-server/

### install
```bash
curl -fsSL https://code-server.dev/install.sh | sh -s -- --dry-run
curl -fsSL https://code-server.dev/install.sh | sh
```
### config
/root/.config/code-server/config.yaml
```
bind-addr: 0.0.0.0:1235
auth: none
cert: false
```
### script
```
code-server /
```

## crontab

```shell
crontab -e
```

```shell
0 0 * * * /home/andy/speedcubing/dbbackup.sh
```

## Jenkins

https://www.jenkins.io/

### install
https://pkg.jenkins.io/debian-stable/
```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install fontconfig openjdk-17-jre
sudo apt-get install jenkins
```

### config
systemctl edit jenkins
```conf
### Editing /etc/systemd/system/jenkins.service.d/override.conf
### Anything between here and the comment below will become the new contents of the file

[Service]
Environment="JENKINS_PORT=1236"
```

### script
systemctl restart jenkins
###

## MySQL

### fix MySQL mysql_native_password
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
FLUSH PRIVILEGES;
```

## Nginx

### config
/etc/nginx/nginx.conf
```cfg
        server {
            listen 25080 ssl;
            server_name domjudge.speedcubing.top;

            ssl_certificate /home/andy/speedcubing/cert/domjudge.speedcubing.top.crt;
            ssl_certificate_key /home/andy/speedcubing/cert/domjudge.speedcubing.top.key;

            location / {
                proxy_pass http://127.0.0.1:12345;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
            }
        }

        server {
            listen 25080 ssl;
            server_name www.speedcubing.top speedcubing.top;

            ssl_certificate /home/andy/speedcubing/cert/speedcubing.top.crt;
            ssl_certificate_key /home/andy/speedcubing/cert/speedcubing.top.key;

            location / {
                proxy_pass http://127.0.0.1:20081;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
            }
        }

        server {
            listen 25080 ssl;
            server_name api.speedcubing.top;

            ssl_certificate /home/andy/speedcubing/cert/api.speedcubing.top.crt;
            ssl_certificate_key /home/andy/speedcubing/cert/api.speedcubing.top.key;


            location / {
                proxy_pass http://127.0.0.1:20082;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
            }
        }

        server {
            listen 1234;
            client_max_body_size 4096M;
            server_name db.speedcubing.top;

            root /usr/share/phpmyadmin;
            index index.php index.html index.htm;

            # Handle PHP scripts
            location ~ \.php$ {
                fastcgi_split_path_info ^(.+\.php)(/.+)$;
                fastcgi_pass unix:/run/php/php-fpm.sock; # Adjust to your PHP version, e.g., php7.4-f>
                fastcgi_index index.php;
                include fastcgi_params;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                fastcgi_param PATH_INFO $fastcgi_path_info;
            }
        }
```
### script
```
systemctl restart nginx
```

## PHP

### config
/etc/php/8.2/fpm/php.ini
```
upload_max_filesize=4096M
post_max_size=4096M
```
### script
```
systemctl restart php8.2-fpm
```

## phpMyAdmin

### config
/etc/phpmymyadmin/config.inc.php
```php
$cfg['Servers'][$i]['auth_type'] = 'config';
$cfg['Servers'][$i]['user'] = 'root';
$cfg['Servers'][$i]['password'] = 'root';
$cfg['Servers'][$i]['controluser'] = 'root';
$cfg['Servers'][$i]['controlpass'] = 'root';
```

## Java

```shell
sudo apt install openjdk-17-jre
```