By Abdullah Alsubhy
https://github.com/abd1407/linuxProject


Ubuntu-Linux-Server

My Ip 
54.93.194.152

dns
http://54.93.194.152.xip.io/

Private IP:
172.26.15.118

Public IP:
54.93.194.152


secret key for application:
902ddef7fdfd7e6bd4f9ed315d1550c9d9cf5c518910d889


To connect by grader user:
ssh grader@54.93.194.152 -p 2200 -i ~/.ssh/graderKey

To change ssh port:
sudo nano /etc/ssh/sshd_config

To upgrade all installed packs:
sudo apt-get upgrade
sudo apt-get update


To check if firewall is active or not:
sudo ufw status

To stop all incoming traffic:
sudo ufw default deny incoming

To allow all outgoing traffic:
sudo ufw default allow outgoing

To allow port for ssh:
sudo ufw allow ssh
sudo ufw allow 2200/tcp

To allow http port:
sudo ufw allow www

To allow NTP port:
sudo ufw allow 123/tcp
sudo ufw allow NTP

To enable firewall:
sudo ufw enable


To install apache for web application server:
sudo apt-get install apache2


To install mod_wsgi: 
sudo apt-get install libapache2-mod-wsgi


To restart Apache:
sudo apache2ctl restart


To creat WSGI file:
sudo touch /var/www/catalog/catalog.wsgi
sudo nano /var/www/catalog/catalog.wsgi

code:
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0, "/var/www/catalog")
from catalog import app as application
application.secret_key = '902ddef7fdfd7e6bd4f9ed315d1550c9d9cf5c518910d889'



To add new user grader:
sudo adduser grader


To grant soudo permission to grader user:
sudo usermod -a -G sudo grader
sudo cp /etc/sudoers.d/ubuntu /etc/sudoers.d/grader
sudo nano /etc/sudoers.d/grader
and edit this file to change name of sudo user

To make .ssh for 
sudo mkdir /home/grader.ssh

Create new privet key:
ssh-keygen
/home/ubuntu/.ssh/graderKey.pub

To change permission of .ssh and key file;
chmod 700 .ssh
chmod 644 .ssh/authorized_keys


To login by grader user
ssh grader@54.93.194.152 -p 2200 -i ~/.ssh/graderKey


To change local time of server to UTC:
sudo dpkg-reconfigure tzdata
Help Link: https://askubuntu.com/questions/138423/how-do-i-change-my-timezone-to-utc-gmt



To install PostgreSQL:
sudo apt-get install postgresql

To login in main user for psql:
sudo su - postgres

To install Git:
apt-get install git-core


To Creat database and user in psql:
create database catalog;
create user catalog with encrypted password 'catalog';
grant all privileges on database catalog to catalog;



To install Python:
sudo add-apt-repository ppa:jonathonf/python-3.6
sudo apt-get install python3.6

To install pip:
sudo apt install python-pip

To install SQLAlchemy:
sudo -H pip install SQLAlchemy
pip install Flask-SQLAlchemy

To install Flask:
sudo  pip install flask==0.9
sudo  pip install Flask-Login==0.1.3


To install oauth2client to use Google login:
sudo -H pip install oauth2client


When you find error with pip you can reinstall it by this command:
sudo python -m pip uninstall pip && sudo apt install python-pip --reinstall

To install request for python:
sudo pip install requests

Folder that contain config file to handle requests:
sudo nano /etc/apache2/sites-available/000-default.conf

add this code

     ServerName 54.93.194.152
        DocumentRoot /var/www/catalog
        ServerAdmin admin@54.93.194.152
        WSGIDaemonProcess catalog
        WSGIScriptAlias / /var/www/catalog/catalog.wsgi
        <Directory /var/www/catalog>
                WSGIProcessGroup catalog
                WSGIApplicationGroup %{GLOBAL}
                Order allow,deny
                Allow from all
        </Directory>



To check apache error logs:
sudo cat /var/log/apache2/error.log



To stop remote login of the root user:
edit file:  /etc/ssh/sshd_config
PermitRootLogin no


Some Help links:
https://stackoverflow.com/
https://askubuntu.com
http://flask.pocoo.org/docs/1.0/deploying/

Udacity Slack Channels
