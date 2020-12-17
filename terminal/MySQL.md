links:

https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-18-04

https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04

https://devanswers.co/how-to-reset-mysql-root-password-ubuntu/

# Removing MySQL

```bash
sudo apt-get remove --purge mysql*
sudo apt-get autoremove
sudo apt-get autoclean
```

```
sudo autoremove
```

Whenever you install an application (using `apt-get`) the  system will also install the software that this application depends on.  It is common in Ubuntu/Linux that applications share the same libraries. When you remove the appplication the dependency will stay on your  system. 

So `apt-get autoremove` will remove those dependencies  that were installed with applications and that are no longer used by  anything else on the system. 

# Password reset

```bash
drop user admin@localhost;
flush privileges;
create user admin@localhost identified by 'admins_password'
```

or

## (Optional) Adjusting User Authentication and Privileges

In Ubuntu systems running MySQL 5.7 (and later versions), the **root** MySQL user is set to authenticate using the `auth_socket` plugin by default rather than with a password. This allows for some  greater security and usability in many cases, but it can also complicate things when you need to allow an external program (e.g., phpMyAdmin) to access the user.

In order to use a password to connect to MySQL as **root**, you will need to switch its authentication method from `auth_socket` to `mysql_native_password`. To do this, open up the MySQL prompt from your terminal:

```
sudo mysql
```

Next, check which authentication method each of your MySQL user accounts use with the following command:

```
SELECT user,authentication_string,plugin,host FROM mysql.user;
Output+------------------+-------------------------------------------+-----------------------+-----------+
| user             | authentication_string                     | plugin                | host      |
+------------------+-------------------------------------------+-----------------------+-----------+
| root             |                                           | auth_socket           | localhost |
| mysql.session    | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| mysql.sys        | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| debian-sys-maint | *CC744277A401A7D25BE1CA89AFF17BF607F876FF | mysql_native_password | localhost |
+------------------+-------------------------------------------+-----------------------+-----------+
4 rows in set (0.00 sec)
```

In this example, you can see that the **root** user does in fact authenticate using the `auth_socket` plugin. To configure the **root** account to authenticate with a password, run the following `ALTER USER` command. Be sure to change `password` to a strong password of your choosing, and note that this command will change the **root** password you set in Step 2:

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

Then, run `FLUSH PRIVILEGES` which tells the server to reload the grant tables and put your new changes into effect:

```
FLUSH PRIVILEGES;
```

Check the authentication methods employed by each of your users again to confirm that **root** no longer authenticates using the `auth_socket` plugin:

```
SELECT user,authentication_string,plugin,host FROM mysql.user;
Output+------------------+-------------------------------------------+-----------------------+-----------+
| user             | authentication_string                     | plugin                | host      |
+------------------+-------------------------------------------+-----------------------+-----------+
| root             | *3636DACC8616D997782ADD0839F92C1571D6D78F | mysql_native_password | localhost |
| mysql.session    | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| mysql.sys        | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
| debian-sys-maint | *CC744277A401A7D25BE1CA89AFF17BF607F876FF | mysql_native_password | localhost |
+------------------+-------------------------------------------+-----------------------+-----------+
4 rows in set (0.00 sec)
```

You can see in this example output that the **root** MySQL user now authenticates using a password. Once you confirm this on your own server, you can exit the MySQL shell:

```
exit
```





# Issue with connecting via workbench



Your connection attempt failed for user 'root' to the MySQL server at localhost:3306:

>  An AppArmor policy prevents this sender from sending this message to this recipient; type="method_call", sender=":1.125" (uid=1000 pid=7944 comm="/snap/mysql-workbench-community/5/usr/bin/mysql- wo" label="snap.mysql-workbench-community.mysql-workbench- community (enforce)") interface="org.freedesktop.Secret.Service" member="OpenSession” error name="(unset)" requested_reply="0" destination=":1.13" (uid=1000 pid=2044 comm="/usr/bin/gnome- keyring-daemon --daemonize --login" label="unconfined")

```bash
sudo snap connect mysql-workbench-community:password-manager-service :password-manager-service
```