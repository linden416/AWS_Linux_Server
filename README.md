# Project: Linux Server Configuration
## Student: Gordon Seeler / gs6687@att.com
### Date: 2-11-2018 

## Project Files
|File|Description|
|----|-----------|
|GraderKey|Grader account's private key for key based authentication using ssh|
|myCatalogApp_Readme.MD|A public copy of my Readme.MD from my CatalogApp project respository|

## Project Summary

The Item Catalog web project was ported to the internet on a<br>
Linux server running Ubuntu in the Amazon AWS cloud services.

I procured this cloud server and was required to lock it down<br>
to specifications, make available for Udacity reviewer, and host<br>
the prior project submission **Catalog App**.

The server is tightly locked down for only **ssh**, **www**, and **ntp**<br>
incoming requests.

A user account, **grader**, has been created for a Udacity reviewer<br>
to access server with **sudo** privileges.

## The IP address and SSH port of Linux server

The reviewer can access my AWS Linux server at: **35.171.85.15**

The port has been changed from the default, now using **2200**

Sample invocation:<br>
**ssh -i graderKey grader@35.171.85.15 -p 2200**

The passphrase response to the prompt is **Udacity**:<br>
Enter passphrase for key 'graderKey': Udacity

The private key **graderKey** has been added to this repository for reviewer.

## The complete URL to my Catalog Application on Linux Server

The URL to the main page of the Item Catalog web site is:<br>
http://35.171.85.15.xip.io/

A public copy of my Readme.MD that I submitted for the Catalog Application<br>
project has been made available for you called **myCatalogApp_Readme.MD**.<br>
It explains everything you need to know about the application as was required<br>
for the project submission. My Catalog Application repository is private.

One notable change is the replacing of database engine from SQLite to PostgreSQL.

## A summary of software Installed

|Software|Description|
|--------|-----------|
|sudo apt install python3-pip|pip3 Python3 module installer|
|sudo apt-get install apache2|Apache2 Web Server|
|sudo apt-get install libapache2-mod-wsgi-py3|Apache2 mod_wsgi for Python3|
|sudo apt-get install postgresql|PostgreSQL Database|
|sudo apt-get install finger|finger|
|sudo apt-get install ntp|ntp|
|pip3 install Flask==1.0.2|Flask Python3 module|
|pip3 install Flask-HTTPBasicAuth==1.0.1|Flask-HTTPBasicAuth Python3 module|
|pip3 install Flask-HTTPAuth==3.2.4|Flask-HTTPAuth Python3 module|
|pip3 install psycopg2==2.7.6.1|psycopg2 Python3 module|
|pip3 install SQLAlchemy==1.2.15|SQLAlchemy Python3 module|
|pip3 install oauth2client==4.1.3|oauth2client Python3 module|
|pip3 install passlib==1.7.1|passlib Python3 module|

## Configuration Changes

### Changes in support of Web Application
 1. Created a new directory for the Catalog application: **/var/www/catalog**
 2. Cloned my Catalog App from GitHub
 3. Removed Git files/overhead from directory
 4. Renamed project.py to catalog.py
 5. Created new **catalog.wsgi** file to be configured with Apache2 for WSGI
 6. Created new Google OAuth2 Client Secret file for app **Apache-CatalogApp** 
 7. Updated both catalog.py and suptOAuth2.py making client secret file an absolute path.
 8. Updated catalog.py removing the code in __main__ that ran on port 8000 and established app secret key.
 9. Updated both data_model.py and suptDBFxns.py replacing database engine to PostgreSQL.
10. Updated template file login.html specifying new ClientId established from step #6 above.
11. Updated the Apache /etc/apache2/sites-enabled/000-default.conf:
	- Configured WSGI connection to my CatalogApp
	- Configured WSGI Daemon to run as **1 process** to avoid isolating session data<br>
	which would happen if multiple processes were handling page requests. 
12. Created both a **catalog** user account and database in PostgreSQL:
	- postgres=# create user catalog with password 'Udacity';
   	- postgres=# create database catalog;
   	- postgres=# grant all privileges on database catalog to catalog;
 
 ### Changes to secure Linux server
  1. Activated **ufw** Firewall
  2. Setup default blocking of all incoming requests
  3. Setup default allowing all outgoing requests
  4. Setup specific rules on ports/programs:
    	- Allow ssh
	- Allow 2200/tcp
	- Allow web
    	- Allow ntp
    	- Allow 123/udp
  5. Enabled service
  6. Performed following steps to lock down **ssh**
  7. Removed **ssh** Password Authentication, Remote Root Login, and Default Port
  8. Updated the sshd_config file:
  	- Changed port to 2200
	- Set PasswordAuthentication to no
	- Set PermitRootLogin to no
  9. Performed following steps to update system software:
  	- Ran apt-get update
	- Ran apt-get upgrade
     
 ### Changes for creating new user
  1. Added new user **grader**
  2. Added new file **grader** to the **/etc/sudoers.d** directory
  3. Edited newly created **grader** file to allow all sudo access
  4. Created a **.ssh** directory in **grader's** home directory
  5. Created new **authorized_keys** file in **.ssh** directory
  6. Copied and pasted the **grader's** public key<br>
     (this will be provided in project submission Note's to Reviewer field)
  

## List of any third-party resources used to complete this project

[How do I disable SSH login for the root user?](https://mediatemple.net/community/products/dv/204643810/how-do-i-disable-ssh-login-for-the-root-user)<br>
[Udacity Knowledgebase](https://knowledge.udacity.com/questions21110)<br>
[Wildcard DNS Using xip.io](https://www.getmura.com/blog/wildcard-dns-using-xipio/)<br>
[NTP Info - install and config](https://www.tecmint.com/install-and-configure-ntp-server-client-in-debian/)<br>
[NTP Info - ntp client](https://www.cyberciti.biz/faq/linux-unix-bsd-is-ntp-client-working/)<br>
[NTP Info - how to restart](https://askubuntu.com/questions/1009729/unable-to-start-ntpd-service)<br>
[How to check opened/closed ports on my computer?](https://askubuntu.com/questions/538208/how-to-check-opened-closed-ports-on-my-computer)<br>
[Linux Man Pages for sshd_config](http://man7.org/linux/man-pages/man5/sshd_config.5.html)<br>
[WSGI.org](https://wsgi.readthedocs.io/en/latest/)<br>
[mod_wsgi Document User Guides Installation](https://modwsgi.readthedocs.io/en/develop/user-guides/checking-your-installation.html#python-installation-in-use)<br>
[mod_wsgi Document User Guides Installation Issues](https://modwsgi.readthedocs.io/en/develop/user-guides/installation-issues.html)<br>
[mod_wsgi Document User Guides - Application Working Directory](https://modwsgi.readthedocs.io/en/develop/user-guides/application-issues.html#application-working-directory)<br>
[Apache.org](http://httpd.apache.org/)<br>
[Apache.org Configuration](http://httpd.apache.org/docs/current/configuring.html)<br>
[PostgreSQL.org](http://www.postgresql.org/)<br>
[PostgreSQL.org Psql](http://postgresguide.com/utilities/psql.html)<br>
[mod_wsgi (Apache)](http://flask.pocoo.org/docs/1.0/deploying/mod_wsgi/)<br>
[DigitalOcean - How To Deploy a Flask Application on an Ubuntu VPS](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)<br>
[BogoToBogo - Flask Hello World App with Apache WSG](https://www.bogotobogo.com/python/Flask/Python_Flask_HelloWorld_App_with_Apache_WSGI_Ubuntu14.php)<br>
[StackOverflow - Logins stop working when switching to wsgi with Flask, Flask login, mod-wsgi](https://stackoverflow.com/questions/48513139/logins-stop-working-when-switching-to-wsgi-with-flask-flask-login-mod-wsgi)<br>
[A2 Hosting - How to disable SSH logins for the root account](https://www.a2hosting.com/kb/getting-started-guide/accessing-your-account/disabling-ssh-logins-for-root)<br>

