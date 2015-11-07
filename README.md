# fullstack_proj5
## Overview
The goal of this project was to host the web application developed for project 3 on a publicly accessible VM in Amazon's EC2 cloud. The application is served using an Apache web server and WSGI and the VM is configured to make it more secure.
The IP address of the VM is 52.32.159.106.  It can be accessed using ssh on port 2200.  The URL is http://ec2-52-32-159-106.us-west-2.compute.amazonaws.com.
## VM configuration
Here are the configuration changes that were made to the VM:
* Updated all currently installed packages (apt-get upgrade, apt-get update)
* Created a new user, grader, and granted this user sudo permissions
* Changed the sshd default port to 2200 and disabled the ability for the root user to ssh into the VM (/etc/ssh/sshd_config)
* Enabled the firewall, allowing incoming requests on ports 2200 (ssh), 123 (ntp) and 80 (http) (sudo ufw allow, sudo ufw enable)
* Installed the following additional packages using apt-get install
	* apache2 (2.4.7)
	* libapache2-mod-wsgi (3.4)
	* postgresql (9.3)
	* git (1:1.9.1)
	* python-pip (1.5.4)
	* postgresql-contrib (9.3)
	* libpq-dev (9.3)
	* python-dev (2.7.5)
* Installed the following python modules using pip install
	* Flask (0.10.1)
	* oauth2client (1.5.1)
	* psycopg2 (2.6.1)
	* SQLAlchemy (1.0.9)

## Web server/WSGI configuration
* Added the following line to /var/apache2/sites-available/000-default.conf: WSGIScriptAlias / /var/www/restaurantapp/app.wsgi
* Created the app.wsgi

## Source code changes
The code is based on the source provided in the Udacity Full Stack Foundations and Authentication & Authorization courses.  It uses python 2.7, the flask framework and facebook and google 3rd party authentication API's.  The original code used a sqlite database; changes were made to use a postgresql database.  In addition a few changes were required to use the newer release of the OAuth2Client.  The URL also had to be provided on the google and facebook developer consoles for this application.

The postgresql database (restaurantmenuwithusers) was created by the postgres user and the www-data user was granted public schema permissions on it.  www-data is the user used by the web app to access the database.
