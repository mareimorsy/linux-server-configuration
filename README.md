# Linux server coniguration

> You will take a baseline installation of a Linux distribution on a virtual machine and prepare it to host your web applications, to include installing updates, securing it from a number of attack vectors and installing/configuring web and database servers.

## The IP address and SSH port
```
ssh ubuntu@54.187.22.85 -p 2200 -i linuxCourse.pem
```
## The complete URL to item catalog app.
http://ec2-54-187-22-85.us-west-2.compute.amazonaws.com/

## Add grader user
```
sudo adduser grader
sudo touch /etc/sudoers.d/grader
sudo nano /etc/sudoers.d/grader
```
paste `grader ALL=(ALL) NOPASSWD: ALL`

## set SSH authentication
```
su - grader
mkdir .ssh
touch .ssh/authorized_keys
nano .ssh/authorized_keys
```
paste the public key which has genereted locally using `sshkeygen`
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCXDw0BqYM9T1/pI2/+lHXSe+TMq0Pm49DLfFmFgF32gBU84TbGPMyhhw+czkTp8qA+dOVmtP3zof4c6u+QcGOEd5PRnAkVNzf0vWiWbM+q61G4PCX0BZI0Bi/Va0sfs/vhm5NIHML8dOKhSItEnMf1UN+LBOfPzDd8sEVeptqxDzMgfle5+Nba4cd79unzhJGO0NRz8ekRem8ZGPBqnzzx4CY5qg4S+Wh7/FOjcfXjMjsCN4zVsflWxbEp0FgV/jv8Tx3pfZArOK7/oDonpFIlXb1fdqebqQwAjUv/zBLL/A1+GeLRsqMCavalYKrG8P+ammGSx+WpE58NfeGH3f4/ Marei@DESKTOP-SO6389O
```
Modify the permissions
```
chmod 700 .ssh
chmod 644 .ssh/authorized_keys
```
## Change the SSH port from 22 to 2200
```
sudo nano /etc/ssh/sshd_config
```
Restart SSH
```
service ssh restart
```
Now you can login using
```
ssh grader@54.187.22.85 -p 2200 -i graderKey.pem
```
## Update system packages
```
sudo apt-get update
sudo apt-get upgrade
```
## Configure the Uncomplicated Firewall (UFW)
```
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 2200/tcp
sudo ufw allow www
sudo ufw allow ntp
sudo ufw enable
```
## Install git
```
sudo apt-get install git
```
## Install PIP
```
sudo apt-get install python-pip
```
## Install the following python packages
```
pip install Flask
pip install SQLAlchemy
pip install --upgrade oauth2client
pip install requests
```
## Clone Item catalog project
```
git clone https://github.com/mareimorsy/udacity-nanodegree-item-catalog.git
cd udacity-nanodegree-item-catalog/
```
Edit Authorized JavaScript origins
## Run a Python script in the background even after I logout SSH
```
sudo nohup python app.py
```
