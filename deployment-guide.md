# ⚙️ Step-by-Step Maven + Tomcat Deployment Guide

This guide explains how to install Java, Maven, and Tomcat on a Linux server, build a Maven project, and deploy it on Tomcat.

---

## ☕ Java Installation

**Step 1: Switch to root user**
```bash
sudo su -
```

**Step 2: Update system packages**
```bash
apt update -y
```
**Step 3: Install Java**
```bash
apt install openjdk-17-jre-headless -y
```
**Step 4: Check Java version**
```bash
java --version
```

## 🧰 Maven Installation

**Step 5: Download Maven from the official website**
```bash 
wget https://dlcdn.apache.org/maven/maven-3/3.9.11/binaries/apache-maven-3.9.11-bin.tar.gz
```
**Step 6: Extract the Maven tar file**
```bash
tar -zxvf apache-maven-3.9.11-bin.tar.gz
```
**Step 7: Remove the tar file and check extracted folder**
```bash
rm -rf apache-maven-3.9.11-bin.tar.gz
ls
```


**Step 8: Rename the Maven folder**
```bash
mv apache-maven-3.9.11 maven
```

**Step 9: Open .bashrc and add Maven path**
```bash
vi .bashrc
```

Add the following line at the end of the file:
```bash
export PATH=/root/maven/bin:$PATH
```

**Step 10: Reload .bashrc**
```bash 
source .bashrc
```

**Step 11: Check Maven version**
```bash
mvn --version
```

## 🧱 Maven Project Setup

**Step 12: Clone the Maven project repository**
```bash
git clone https://github.com/Pavi2535/sample-maven-project.git
```

**Step 13: Go inside the Maven project folder**
```bash
cd sample-maven-project
```

**Step 14: Clean and build the project**
```bash
mvn clean package -DskipTests
```

## 🐱‍🏍 Tomcat Installation

**Step 15: Go back to the root directory**
```bash
cd ..
```

**Step 16: Download Tomcat**
```bash
wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.48/bin/apache-tomcat-10.1.48.tar.gz
```

**Step 17: Extract the Tomcat tar file**
```bash
tar -zxvf apache-tomcat-10.1.48.tar.gz
```

**Step 18: Rename the Tomcat folder**
```bash
mv apache-tomcat-10.1.48 apache
```

**Step 19: Go inside the Tomcat folder**
```bash
cd apache
``` 

## 🔐 Tomcat Configuration

**Step 20: Navigate to the configuration folder**
```bash
cd conf
```

**Step 21: List the files**
```bash
ls
```

**Step 22: Open the tomcat-users.xml file**
```bash
vi tomcat-users.xml
```

**Add the following roles and user before the closing </tomcat-users> tag:**
```bash
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="manager-jmx"/>
<role rolename="manager-status"/>
<user username="admin" password="admin" roles="manager-gui,manager-script,manager-jmx,manager-status"/>
```

**Step 23: Go back to Tomcat’s main folder**
```bash
cd ..
```

**Step 24: Edit the Manager App configuration to allow access**
```bash
vi webapps/manager/META-INF/context.xml
```

**Comment out the following section: **
```bash
<!--
**<CookieProcessor className="org.apache.tomcat.util.http.Rfc6265CookieProcessor" sameSiteCookies="strict" />
**<Valve className="org.apache.catalina.valves.RemoteAddrValve"
       allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
**-->
```

 ## 🚀 Starting Tomcat Server

**Step 25: Go to the bin folder**
```bash
cd bin
```

**Step 26: List the available scripts**
```bash
ls
```

**Step 27: Start the Tomcat server**
```bash
sh startup.sh
```

**Step 28: Open your browser and visit**
```bash
http://<public-instance-ip>:8080
```

**You’ll see the Tomcat welcome page. Go to Manager App, log in with:**

Username: admin
Password: admin

You’ll see the list of webapps (but not your project yet)

## ⚙️ Deploying the WAR File

**Step 29: Stop the Tomcat server**
```bash
sh shutdown.sh
```

**Step 30: Go back to the root directory**
```bash
cd ..
```

**Step 31: Copy the project WAR file to Tomcat’s webapps folder**
```bash
cp sample-maven-project/target/students.war apache/webapps/
```

**Step 32: Restart the Tomcat server**
```bash
sh apache/bin/startup.sh
```

## ✅ Deployment Complete

**Now, open your browser and navigate to:**
```bash
http://<public-instance-ip>:8080/students
```

**🎉 You should see your deployed Maven web application running successfully on Tomcat.**
