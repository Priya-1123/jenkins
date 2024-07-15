# jenkins


#Installing Jenkins
#First, update the default Ubuntu packages lists for upgrades with the following command:

sudo apt-get update
#Then, run the following command to install JDK 11:

sudo apt-get install openjdk-11-jdk
#Now, we will install Jenkins itself. Issue the following four commands in sequence to initiate the installation from the Jenkins repository:

curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update

sudo apt-get install jenkins
#Once that’s done, start the Jenkins service with the following command:

sudo systemctl start jenkins.service
#To confirm its status, use:

sudo systemctl status jenkins
#With Jenkins installed, we can proceed with adjusting the firewall settings. By default, Jenkins will run on port 8080.

#In order to ensure that this port is accessible, we will need to configure the built-in Ubuntu firewall (ufw). To open the 8080 port and enable the firewall, use the following commands:

sudo ufw allow 8080
sudo ufw enable
#Once done, test whether the firewall is active using this command:

sudo ufw status
#With the firewall configured, it’s time to set up Jenkins itself. Type in the IP of your EC2 along with the port number. The Jenkins setup wizard will open.

#To check the initial password, use the cat command as indicated below:

sudo cat /var/lib/jenkins/secrets/initialAdminPassword
#All Set! You can now start automating...

2. How to Configure and Run Jenkins Behind Apache Reverse Proxy?
#Installing Apache Install Apache from Repo

sudo apt-get update
sudo apt-get install apache2 -y
#Enable proxy, proxy_http, headers module

sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod headers
#Edit Apache Configuration file

cd /etc/apache2/sites-available/
sudo vim jenkins.conf
#Then, In the file enter the following code snippet to make the Apache works for Jenkins. Then, In this ServerName should be your domain name, ProxyPass should point your localhost point to Jenkins (Port 8080) and ProxyPassReverse should be added for both localhost address and Domain address. In the block, we need to give access to the apache to handle the Jenkins.

 
#Enable and Restart Jenkins

sudo a2ensite jenkins
sudo systemctl restart apache2
sudo systemctl restart jenkins
#Configuring Firewall

sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
#Now, enable firewall by passing following command.


