# Linux Server Setup (Apache, MySQL, PHP)

## Introduction
This guide provides a comprehensive walkthrough for setting up a Linux server with Apache, MySQL, and PHP. It also covers essential configurations, including service management, permissions setup, and database handling, ensuring your server is ready for web development. Additionally, basic Linux commands are included for convenience.

## Update System
Run the following commands to ensure your system is updated:
```bash
sudo apt update
sudo apt upgrade -y
```

## Service Management

- **Check service status:**
  ```bash
  systemctl status service_name
  ```
- **Start service:**
  ```bash
  sudo systemctl start service_name
  ```
- **Restart service:**
  ```bash
  sudo systemctl restart service_name
  ```
- **Stop service:**
  ```bash
  sudo systemctl stop service_name
  ```
- **Enable service to start on boot:**
  ```bash
  sudo systemctl enable service_name
  ```

## Install Apache
```bash
sudo apt install apache2
```

## Install MySQL
```bash
sudo apt install -y mysql-server
```

## Install Git
```bash
sudo apt install -y git
```

## Install PHP
```bash
sudo apt -y install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt install -y php8.2 php8.2-cli php8.2-fpm php8.2-common php8.2-mysql php8.2-curl php8.2-mbstring php8.2-xml php8.2-bcmath php8.2-zip php8.2-intl php8.2-gd php8.2-opcache php8.2-readline php8.2-soap
```

## Install Composer
```bash
curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php
sudo php /tmp/composer-setup.php --install-dir=/usr/bin --filename=composer
```

## Set Permissions for Laravel
Ensure the necessary permissions are set for Laravel to operate smoothly:
```bash
sudo chgrp -R www-data /var/www/html/abasyn-web
sudo chmod -R 775 /var/www/html/abasyn-web/storage
sudo chmod -R 775 /var/www/html/abasyn-web/bootstrap/cache
```

## Database Setup
Follow these steps to configure your database:
```bash
sudo mysql -u root -p
Create database db_name;
source /path/to/your/sql/file.sql;
GRANT ALL PRIVILEGES ON db_name.* TO 'root'@'localhost';
```

## Clone Repository with Username and Token
Clone your repository securely:
```bash
git clone https://username:token@github.com/username/repo.git
```

## Check Installed PHP Versions
Manage PHP versions as needed:
```bash
dpkg --list | grep php
sudo apt remove --purge php7.4 php7.4-*
sudo apt autoremove --purge
sudo apt clean
```

## SSH Service Management
- **Check if SSH service is running:**
  ```bash
  sudo systemctl status ssh
  ```
- **Start SSH service:**
  ```bash
  sudo systemctl start ssh
  ```
- **Enable SSH on boot:**
  ```bash
  sudo systemctl enable ssh
  ```

## Apache Configurations
1. Navigate to Apache configurations:
   ```bash
   cd /etc/apache2/sites-available
   sudo nano laravel_project.conf
   ```
2. Add the following VirtualHost configuration:
   ```apache
   <VirtualHost *:80>
       ServerName [thedomain.com] or [ip]
       ServerAdmin webmaster@thedomain.com
       DocumentRoot /var/www/html/example/public

       <Directory /var/www/html/example>
           AllowOverride All
       </Directory>
       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>
   ```
3. Disable the default configuration:
   ```bash
   sudo a2dissite 000-default.conf
   ```
4. Enable the new virtual host:
   ```bash
   sudo a2ensite laravel_project
   ```
5. Enable Apache rewrite module and restart:
   ```bash
   sudo a2enmod rewrite
   sudo systemctl restart apache2
   ```

## Basic Linux Commands
- **Print working directory:**
  ```bash
  pwd
  ```
- **Copy file:**
  ```bash
  cp .env.example .env
  ```
- **Remove directory:**
  ```bash
  sudo rm directory_path
  ```
- **Remove non-empty directory:**
  ```bash
  sudo rm -rf directory_path
  ```
- **Check Composer location:**
  ```bash
  which composer
  ```
- **Check PHP location:**
  ```bash
  where php
  ```
- **Remove package:**
  ```bash
  sudo apt remove package_name
  ```
- **Reboot system:**
  ```bash
  sudo reboot
  ```
