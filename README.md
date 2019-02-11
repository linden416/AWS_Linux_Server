# Project: Linux Server Configuration
## Student: Gordon Seeler / gs6687@att.com
### Date: 2-11-2018 

## Project Files
|File|Description|
|----|-----------|
|GraderKey|Grader account's private key for key based authentication using ssh|
|myCatalogApp_Readme.MD|A public copy from my private CatalogApp respository|

## Project Summary

The Item Catalog web project was ported to the public internet.
A Linux server running Ubuntu in the Amazon AWS cloud services.

The server is tightly locked down for only ssh, web, and ntp 
incoming requests.

A user account, **grader**, has been created for Udacity to access
server with **sudo** privileges.

## The IP address and SSH port of Linux server

The reviewer can access my AWS Linux server at: 35.171.85.15
The port has been changed, now using 2200

Here is a sample invocation:
ssh -i graderKey grader@35.171.85.15 -p 2200

The passphrase respone to the prompt is **Udacity**:
Enter passphrase for key 'graderKey': Udacity

The private key **graderKey** has been added to this repository for reviewer.

## The complete URL to my Catalog Application on Linux Server

The URL to the splash / main page of the Item Catalog web site is:
http://35.171.85.15.xip.io/

A public copy of my Readme.MD that I submitted for the Catalog Application project
has been made available for you called **myCatalogApp_Readme.MD**. It explains
everything you need to know about the application as was required for the 
project submission. My Catalog Application repository is private.

One notable change is the replacing of database ending from SQLite to PostgreSQL.

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
 5. Created new catalog.wsgi file to be configured in Apache2 for WSGI
 6. Created new Google OAuth2 Client Secret file for app **Apache-CatalogApp** 
 7. Updated both catalog.py and suptOAuth2.py making path to client secret file absolute.
 8. Updated catalog.py removing the code in __main__ that ran on port 8000 and established app secret key.
 9. Updated both data_model.py and suptDBFxns.py replacing database engine to PostgreSQL.
10. Updated template file login.html specifying new ClientId established from step #6 above.
11. Updated the Apache /etc/apache2/sites-enabled/000-default.conf: 
	- Configured WSGI connect to CatalogApp
	- Configured WSGI Daemon to run as 1 process to avoid isolating session data
		which would happen if multipler processes handled page requests. 
12. Created both a **catalog** user account and database in PostgreSQL:
    postgres=# create user catalog with password 'Udacity';
    postgres=# create database catalog;
    postgres=# grant all privileges on database catalog to catalog;
 
 ### Changes to secure Linux server
  1. Activated **ufw** Firewall
  2. Setup default blocking of all incoming requests
  3. Setup default allowing all outgoing requests
  4. Setup specific rules on ports/programs:
    a) Allow ssh 
    b) Allow 2200/tcp 
    c) Allow web
    d) Allow ntp
    e) Allow 123/udp
  5. Enabled service
  
  6. Removed Password Authentication, Remote Root Login, and Default Port
  7. Updated the sshd_config file:
     a) Change Port to 2200
     b) Set PasswordAuthentication to No
     c) Set PermitRootLogin to No
     
  8. Update and Upgrade System Software Packages
  9. Ran apt-get update
 10. Ran apt-get upgrade
     
 ### Changes for creating new user
  1. Added new user **grader**
  2. Added new file **grader** to the **/etc/sudoers.d** directory
  3. Edited newly created **grader** file to allow all sudo access
  4. Created a **.ssh** directory in **grader's** home
  5. Created new **authorized_keys** file in **.ssh**
  6. Copy and pasted the **grader's** public key (provided in project submission Note's to Reviewer field)
  

## List of any third-party resources used of to complete this project

https://mediatemple.net/community/products/dv/204643810/how-do-i-disable-ssh-login-for-the-root-user
https://knowledge.udacity.com/questions21110
https://www.getmura.com/blog/wildcard-dns-using-xipio/
https://www.tecmint.com/install-and-configure-ntp-server-client-in-debian/
https://www.cyberciti.biz/faq/linux-unix-bsd-is-ntp-client-working/
https://askubuntu.com/questions/1009729/unable-to-start-ntpd-service
https://askubuntu.com/questions/538208/how-to-check-opened-closed-ports-on-my-computer
http://man7.org/linux/man-pages/man5/sshd_config.5.html
https://wsgi.readthedocs.io/en/latest/
https://modwsgi.readthedocs.io/en/develop/user-guides/checking-your-installation.html#python-installation-in-use
https://modwsgi.readthedocs.io/en/develop/user-guides/installation-issues.html
http://httpd.apache.org/
http://httpd.apache.org/docs/current/configuring.html
http://www.postgresql.org/
http://postgresguide.com/utilities/psql.html
http://flask.pocoo.org/docs/1.0/deploying/mod_wsgi/
http://httpd.apache.org/docs/current/configuring.html
https://modwsgi.readthedocs.io/en/develop/user-guides/installation-issues.html
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
https://www.bogotobogo.com/python/Flask/Python_Flask_HelloWorld_App_with_Apache_WSGI_Ubuntu14.php
http://man7.org/linux/man-pages/man5/sshd_config.5.html
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
https://modwsgi.readthedocs.io/en/develop/user-guides/application-issues.html#application-working-directory
https://stackoverflow.com/questions/48513139/logins-stop-working-when-switching-to-wsgi-with-flask-flask-login-mod-wsgi
https://www.a2hosting.com/kb/getting-started-guide/accessing-your-account/disabling-ssh-logins-for-root

