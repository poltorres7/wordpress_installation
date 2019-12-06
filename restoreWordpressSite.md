## Restore
To restore your site you need to achieve 2 points.
1. [Restore your database from backup](#restore-your-database-from-backup)
2. [Restore your site](#restore-your-site)

I've added a little lab to practice the restore process.
- [Practice example](#practice-example)

----

1.- Restore your database from backup <a name="restoring"></a>
----------
The restore process consists of uncompress your compress database dump, and importing it into your MySQL/MariaDB database:

**Important:** when your want to load the database in your new server it'll load to an **existing** database; ensure that exist your database it doesn't matter if it is empty.
```mysql
# REPLACE               DATABASE-NAME
MariaDB> CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
```

Now upload your backup to your new MySQL server:
```bash
# extract your sql file
[root@lamp-fedora ~]# tar -xjvf wordpress_backup_db.sql.tar.gz
# load you .sql file to your wordpress
[root@lamp-fedora ~]# mysql -h localhost -u user -p wordpress < wordpress_backup_db.sql
```

Now you need to create or config the *user* that will have privileges over that database.
```mysql

# REPLACE             YOUR-SITE       YOUR-USER      YOUR-SERVER               YOUR-PASSWORD-FOR-THIS-DATABASE
MariaDB> GRANT ALL ON wordpress.* TO 'wordpressuser'@'localhost' IDENTIFIED BY 'password';

MariaDB> FLUSH PRIVILEGES;
MariaDB> EXIT;
```

Now you are ready to use this loaded database from your wordpress site.

>If you want to know more or see other options see [Official Documentation](https://wordpress.org/support/article/restoring-your-database-from-backup/)

2.- Restore your site
--------
In the backup process you created a tarball (Compress file) of the wordpress directory of your site. If you want to restore this tarball you need to untar all the directory and put it back again in your *html* directory.
1. Extract the files in your tarball `tar -xjvf YOUR-SITE.tar.gz`
2. Copy the folder of your site to your *hmtl* path `cp YOUR-SITE /var/www/html/`

```bash
# Extract your site
[root@lamp-fedora ~]# tar -xjvf wordpress-site.com.tar.gz
# Copy your site folder to your html path
[root@lamp-fedora ~]# cp wordpress-site.com /var/www/html/
```

Congrats! your site is now allocated in the correct folder.

Now let's review if it has the correct users.
```bash
# THIS IS HOW YOUR HTML FOLDER SHOULD LOOK LIKE
[root@lamp-fedora html]# ls -l
drwxr-xr-x. 5 apache apache     4096 Dec  7 07:38 sitio2.com
[root@lamp-fedora html]# 
```
If you pay attention the user and group is *apache* If you don't have it you can change it with:
```bash
[root@lamp-fedora html]# chown -R apache:apache <YOUR-SITE>
```
We are almost done. You only need to check the configuration of your wp-config.php file. Because you may have changed the:
- WP-DATABASE
- WP-USER
- WP-PASSWORD

After validating these variables you DONE!

Practice example
-------
I have uploaded the backup files of a simple site. You can find it inside the folder [lab1](lab1)
- [sitio2_backup_db.sql](lab1/sitio2_backup_db.sql) (database)
- [sitio2.com.tar.gz](lab1/sitio2.com.tar.gz) (wordpress site folder)

Put in practice your knowledge and improve your skills.
