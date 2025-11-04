🚀 Maven Project Deployment on Tomcat Server

A Complete Step-by-Step Guide

This guide explains how to install Java, Maven, and Tomcat, and how to deploy a Maven project on a Tomcat server.

⚙️ 1. Switch to Root User
sudo su -

🔄 2. Update System Packages
apt update -y

☕ 3. Install Java
apt install openjdk-17-jre-headless -y

🧾 4. Verify Java Installation
java --version

🧰 5. Download and Install Maven
📥 Download Maven
wget https://dlcdn.apache.org/maven/maven-3/3.9.11/binaries/apache-maven-3.9.11-bin.tar.gz

📦 Extract the Archive
tar -zxvf apache-maven-3.9.11-bin.tar.gz

🧹 Remove the Zip File and Check Folder
rm -rf apache-maven-3.9.11-bin.tar.gz
ls

🏷️ Rename the Maven Folder
mv apache-maven-3.9.11 maven

🔧 Add Maven to .bashrc

Open:

vi .bashrc


Add this line at the end:

export PATH=/root/maven/bin:$PATH


Reload:

source .bashrc

✅ Verify Maven Installation
mvn --version

🧱 6. Build Your Maven Project
🧬 Clone the Project Repository
git clone https://github.com/Pavi2535/sample-maven-project.git

📂 Navigate into Project Folder
cd sample-maven-project

🏗️ Clean and Build the Project
mvn clean package -DskipTests

🐱‍🏍 7. Install and Configure Tomcat
📥 Download Tomcat
wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.48/bin/apache-tomcat-10.1.48.tar.gz

📦 Extract the Archive
tar -zxvf apache-tomcat-10.1.48.tar.gz

🏷️ Rename the Tomcat Folder
mv apache-tomcat-10.1.48 apache

📂 Enter Tomcat Directory
cd apache

🔐 8. Configure Tomcat Users

Go to configuration folder:

cd conf
ls


Edit the tomcat-users.xml file:

vi tomcat-users.xml


Add the following lines before </tomcat-users>:

<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="manager-jmx"/>
<role rolename="manager-status"/>
<user username="admin" password="admin" roles="manager-gui,manager-script,manager-jmx,manager-status"/>

⚙️ 9. Update Manager Access Settings

Edit:

vi webapps/manager/META-INF/context.xml


Comment the following lines:

<!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"
 allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->

🚀 10. Start Tomcat Server

Navigate to Tomcat bin folder:

cd ../bin


Start Tomcat:

sh startup.sh


Access in browser:

http://<public-ip>:8080

🧨 11. Deploy Maven Project WAR File

Copy the WAR file to webapps folder:

cp /root/sample-maven-project/target/students.war /root/apache/webapps/


Restart Tomcat:

sh /root/apache/bin/shutdown.sh
sh /root/apache/bin/startup.sh


Access the deployed application:

http://<public-ip>:8080/students

✅ 12. Stop Tomcat Server (Optional)
sh /root/apache/bin/shutdown.sh
