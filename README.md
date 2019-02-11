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

The public copy of Readme.MD I submitted for the Catalog Application project
has been made available for you called **myCatalogApp_Readme.MD**. It explains
everything you need to know about the application as was required for the 
project submission. 

One notable change is the replacing of SQLite to PostgreSQL for the backend database.

## A summary of software Installed

|Software|Description|
|--------|-----------|
|sudo apt install python3-pip|pip3|
|sudo apt-get install apache2|Apache|
|sudo apt-get install libapache2-mod-wsgi-py3|mod_wsgi for Python3|
|sudo apt-get install postgresql|PostgreSQL|
|sudo apt-get install finger|finger|
|sudo apt-get install ntp|ntp|
|pip3 install Flask==1.0.2|Flask|
|pip3 install Flask-HTTPBasicAuth==1.0.1|Flask-HTTPBasicAuth|
|pip3 install Flask-HTTPAuth==3.2.4|Flask-HTTPAuth|
|pip3 install psycopg2==2.7.6.1|psycopg2|
|pip3 install SQLAlchemy==1.2.15|SQLAlchemy|
|pip3 install oauth2client==4.1.3|oauth2client|
|pip3 install passlib==1.7.1|passlib|




