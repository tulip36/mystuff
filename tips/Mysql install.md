Clipped from: https://manjaro-tutorial.blogspot.com/2016/11/install-mysql-server-on-manjaro-1610.html

**MySQL Server on Manjaro**-MySQL Server is a powerful database server used my millions websites around the world. Additionally, many people and company now migrate their database to MySQL Server. I am working on a Gold exploration company and we use MySQL Server as our main database server for the geological data. 

MySQL Server can be installed on most Operating Systems such as Windows and Linux. On this tutorial, I will show you how to install MySQL Server on Manjaro 16.10. Installing MySQl can be done through Terminal using pacman install command.

### Steps to install MySQL Server on Manjaro 16.10

#### Installation for mysql

Open Terminal and type the following command

> sudo pacman -S mysql

Output

> *[dhani@dhani-manjaro ~]$ sudo pacman -S mysql
> :: There are 2 providers available for mysql:
> :: Repository extra
>   1) mariadb
> :: Repository community
>   2) percona-server
> Enter a number (default=1):* 

Type 1 to select mariadb package or simply press Enter. 

Output:

> *Resolving dependencies...
> looking for conflicting packages...
> Packages (4) jemalloc-4.3.1-1  libmariadbclient-10.1.19-1
>        mariadb-clients-10.1.19-1  mariadb-10.1.19-1
> Total Download Size:   19.44 MiB
> Total Installed Size:  172.45 MiB
> :: Proceed with installation? [Y/n] y*

Type Y to confirm the installation. Then pacman will download required files from the official repository. 



#### Initial Configuration

When installation completed, now we need to start MySQL and perform initial configuration. Use this command below instead:

> sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql



#### Start Mariadb Service

> sudo systemctl start mariadb



#### Secure Mariadb installation

> sudo mysql_secure_installation

Output:

> [dhani@dhani-manjaro ~]$ mysql_secure_installation
> NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
>    SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!
> In order to log into MariaDB to secure it, we'll need the current
> password for the root user.  If you've just installed MariaDB, and
> you haven't set the root password yet, the password will be blank,
> so you should just press enter here.
> Enter current password for root (enter for none):
> OK, successfully used password, moving on...
> Setting the root password ensures that nobody can log into the MariaDB
> root user without the proper authorisation.
> Set root password? [Y/n] y
> New password:
> Re-enter new password:
> Password updated successfully!
> Reloading privilege tables..
>  ... Success!
>
> By default, a MariaDB installation has an anonymous user, allowing anyone
> to log into MariaDB without having to have a user account created for
> them.  This is intended only for testing, and to make the installation
> go a bit smoother.  You should remove them before moving into a
> production environment.
> Remove anonymous users? [Y/n] y
>  ... Success!
> Normally, root should only be allowed to connect from 'localhost'.  This
> ensures that someone cannot guess at the root password from the network.
> Disallow root login remotely? [Y/n] n
>  ... skipping.
> By default, MariaDB comes with a database named 'test' that anyone can
> access.  This is also intended only for testing, and should be removed
> before moving into a production environment.
> Remove test database and access to it? [Y/n] y
>  \- Dropping test database...
>  ... Success!
>  \- Removing privileges on test database...
>  ... Success!
> Reloading the privilege tables will ensure that all changes made so far
> will take effect immediately.
> Reload privilege tables now? [Y/n] y
>  ... Success!
> Cleaning up...
> All done!  If you've completed all of the above steps, your MariaDB
> installation should now be secure.
> Thanks for using MariaDB!

Note:

*Usually, Mariadb root user is none (no pasword). You should change the root password for security reason.*



#### Check Mariadb Status

sudo systemctl status mariadb

Output:

> *[dhani@dhani-manjaro ~]$ sudo systemctl status mariadb**[sudo] password for dhani:* *● mariadb.service - MariaDB database server*  *Loaded: loaded (/usr/lib/systemd/system/mariadb.service; disabled; vendor preset: disabled)*  *Active: active (running) since Fri 2016-11-25 20:57:21 WIB; 3min 49s ago* *Process: 2333 ExecStartPost=/bin/sh -c systemctl unset-environment _WSREP_START_POSITION (code=exited, status=0/SUCCESS)* *Process: 2248 ExecStartPre=/bin/sh -c [ ! -e /usr/bin/galera_recovery ] && VAR= ||  VAR=`/usr/bin/galera_recovery`; [ $? -eq 0 ]  && systemctl se* *Process: 2245 ExecStartPre=/bin/sh -c systemctl unset-environment _WSREP_START_POSITION (code=exited, status=0/SUCCESS)* *Main PID: 2303 (mysqld)*  *Status: "Taking your SQL requests now..."*  *Tasks: 27 (limit: 4915)*  *CGroup: /system.slice/mariadb.service*      *└─2303 /usr/sbin/mysqld**
> **Nov 25 20:57:21 dhani-manjaro mysqld[2303]: 2016-11-25 20:57:21 139820239334912 [Note] InnoDB: Highest supported file format is Barracuda.**Nov 25 20:57:21 dhani-manjaro mysqld[2303]: 2016-11-25 20:57:21 139820239334912 [Note] InnoDB: 128 rollback segment(s) are active.**Nov 25 20:57:21 dhani-manjaro mysqld[2303]: 2016-11-25 20:57:21 139820239334912 [Note] InnoDB: Waiting for purge to start**Nov 25 20:57:21 dhani-manjaro mysqld[2303]: 2016-11-25 20:57:21 139820239334912 [Note] InnoDB:  Percona XtraDB (http://www.percona.com) 5.6.32-79.0 s**Nov 25 20:57:21 dhani-manjaro mysqld[2303]: 2016-11-25 20:57:21 139820239334912 [Note] Plugin 'FEEDBACK' is disabled.**Nov 25 20:57:21 dhani-manjaro mysqld[2303]: 2016-11-25 20:57:21 139819646707456 [Note] InnoDB: Dumping buffer pool(s) not yet started**Nov 25 20:57:21 dhani-manjaro mysqld[2303]: 2016-11-25 20:57:21 139820239334912 [Note] Server socket created on IP: '::'.**Nov 25 20:57:21 dhani-manjaro mysqld[2303]: 2016-11-25 20:57:21 139820239334912 [Note] /usr/sbin/mysqld: ready for connections.**Nov 25 20:57:21 dhani-manjaro mysqld[2303]: Version: '10.1.19-MariaDB'  socket: '/run/mysqld/mysqld.sock'  port: 3306  MariaDB Server*

Make sure the status is active. This means that we are successfully installed MySQL Server on Manjaro Linux, 

#### continue ...



Follow these instructions to:

- Create a database named pac
- Create a database user named pacuser, with database password pacuser
- Grant this user all privileges on the pac database

**Note**

It is not required to use the pac database name and pacuser user name. Use different names as desired.

#### Procedure

1. Log on to the host that contains your database.

2. Log on to MySQL/MariaDB as the root database user.

   The default MySQL/MariaDB root database password is blank.

   For example:

   ```
   mysql -u root -p
   ```

3. Create a database named pac.

   **note**

   ​	==create database 必须大写。==

   ```
   mysql> CREATE DATABASE pac;
   ```

4. Create a user named pacuser with the password pacuser and grant this user all privileges on the pac database.

   Ensure the database can be connected to from any host (%) and the local host.

   For example:

   ```
   mysql> GRANT ALL ON pac.* TO pacuser@'%';
   ```
   
5. Extract the schema package.

   ```
   tar -xvf pcc-appcenter-9.1.3-dbschema.tar
   ```

6. Run the schema files for the database that has the name pac.

   mysql>use pac;

   mysql>source DBschema/MySQL/egodata.sql;