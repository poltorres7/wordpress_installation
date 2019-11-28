Instalation process wordpress
===============

```bash
dnf update -y
sudo yum install httpd mariadb mariadb-server php php-json php-common php-mysqlnd php-gd php-xml php-mbstring php-mcrypt php-xmlrpc unzip firewalld wget -y
systemctl start httpd
systemctl start mariadb
systemctl start firewalld

systemctl enable httpd
systemctl enable mariadb
systemctl enable firewalld

mysql_secure_installation
mysql -u root -p
tp://wordpress.org/latest.tar.gz


firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --reload

tar -xzvf latest.tar.gz
ll
rsync -avP ~/wordpress/ /var/www/html/
ll /var/www/html/
mkdir /var/www/html/wp-content/uploads
chown -R apache:apache /var/www/html/*

cd /var/www/html
systemctl restart httpd
vim wp-config.php 

systemctl restart httpd
```