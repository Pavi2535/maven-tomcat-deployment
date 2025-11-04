🚀 Maven Project Deployment on Tomcat Server (Step-by-Step Guide)

This guide explains how to install Java, Maven, and Tomcat, and how to deploy a Maven project on a Tomcat server.

Step 1: Switch to Root User
sudo su -

Step 2: Update System Packages
apt update -y

Step 3: Install Java
apt install openjdk-17-jre-headless -y

Step 4: Verify Java Installation
java --version

Step 5: Download Maven from Official Website
wget https://dlcdn.apache.org/maven/maven-3/3.9.11/binaries/apache-maven-3.9.11-bin.tar.gz

Step 6: Extract the Maven Archive
tar -zxvf apache-maven-3.9.11-bin.tar.gz

Step 7: Remove the Zip File and Check the Extracted Folder
rm -rf apache-maven-3.9.11-bin.tar.gz
ls

Step 8: Rename the Maven Folder
mv apache-maven-3.9.11 maven

Step 9: Add Maven Path to .bashrc

Open the file:

vi .bashrc


Add this line at the end:

export PATH=/root/maven/bin:$PATH

Step 10: Reload the .bashrc File
source .bashrc

Step 11: Verify Maven Installation
mvn --version

Step 12: Clone the Maven Project Repository
git clone https://github.com/Pavi2535/sample-maven-project.git

Step 13: Go Inside the Project Folder
cd sample-maven-project

Step 14: Clean and Build the Project
mvn clean package -DskipTests

Step 15: Go Back to Root Directory
cd ..

Step 16: Download Apache Tomcat
wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.48/bin/apache-tomcat-10.1.48.tar.gz

Step 17: Extract the Tomcat Archive
tar -zxvf apache-tomcat-10.1.48.tar.gz

Step 18: Rename the Tomcat Folder
mv apache-tomcat-10.1.48 apache

Step 19: Go Inside the Tomcat Folder
cd apache

Step 20: Go to Configuration Folder
cd conf

Step 21: List Configuration Files
ls

Step 22: Edit tomcat-users.xml to Add Roles and Users
vi tomcat-users.xml


Add these lines before closing </tomcat-users>:

<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="manager-jmx"/>
<role rolename="manager-status"/>
<user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>

Step 23: Move Back to Tomcat Root Folder
cd ..

Step 24: Edit the context.xml File and Comment Restrictions
vi webapps/manager/META-INF/context.xml


Comment this section:

<!--  <CookieProcessor className="org.apache.tomcat.util.http.Rfc6265CookieProcessor"
                   sameSiteCookies="strict" />
  <Valve className="org.apache.catalina.valves.RemoteAddrValve"
 allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->

Step 25: Navigate to the bin Directory
cd bin

Step 26: List Files in the bin Directory
ls

Step 27: Start the Tomcat Server
sh startup.sh

Step 28: Access Tomcat in Browser

Open:

http://<public-instance-ip>:8080

Step 29: Open the Manager App and Log In
Username: admin
Password: admin


You’ll see all available webapps except your project.

Step 30: Stop the Tomcat Server
sh shutdown.sh

Step 31: Copy Your Project WAR File to Tomcat
cd ..
cp sample-maven-project/target/students.war apache/webapps/

Step 32: Start the Tomcat Server Again
sh apache/bin/startup.sh

Step 33: View the Deployed Project

Open in browser:

http://<public-instance-ip>:8080/students


Your project is now successfully deployed on Tomcat! 🎉
