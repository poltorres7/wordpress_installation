How to backup your wordpress database & web site
=========

This document pretends to guide you in the process of backing up your wordpress database and web site.
You need to execute this two main task:
1. [Backup your wordpress database](#backup-your-wordpress-database)
2. [Backup all the files, themes and plugins of your site](#Backup-all-the-files,-themes-and-plugins-of-your-site)

If you need to restore your site, this maybe useful for you:
1. [Restore your database from backup](#restoring)


## Backup all your wordpress site

1.-Backup your wordpress database
-------
The database stores all the comments, posts and persistent text. That is why is important to backup your database.

There are multiple methods to restore a database like, using a GUI interface like *phpmyadmin, MySQL Workbench* or some kind of plugin in your wordpress, but I personally like doing this with a terminal and the always reliable commands.

```bash
#                        mysql_hostserver  user  database_name  name of your backup file
mysqldump --add-drop-table -h localhost -u user -p wordpress﻿ > wordpress_backup_db.sql

#Optional: if you want compress your backup file
tar -czvf wordpress_backup_db.sql.tar.gz wordpress_backup_db.sql

```
> If you want to know more or see other options see [Oficial Documentation](https://wordpress.org/support/article/backing-up-your-database/)

2.-Backup all the files, themes and plugins of your site
----------
All the files inside your wordpress folder are important to backup your site.

1. Go to the directory where your site is located, for instance `/var/www/html/`
```bash
[root@lamp-fedora ~]# cd /var/www/html/
```

2. If you execute a `ls -l` you should see the folder of your site
```bash
[root@lamp-fedora html]# ls -l
total 12
drwxr-xr-x. 5 apache apache 4096 Dec  7 08:03 localclothes.com
drwxr-xr-x. 5 apache apache 4096 Dec  7 07:00 mxintech.com
drwxr-xr-x. 5 apache apache 4096 Dec  7 07:38 sitio2.com
```

3. The next step is package your site and compress it.
```bash
[root@lamp-fedora html]# tar -cjvf mxintech.com.tar.gz mxintech.com/
```

Congrats! You have restore all the files and databases needed to have a reliable backup.

If you want info for the restore process please check [Restore process](restoreWordpressSite.md)