# Installing and Configuring Tomcat Server

## Power On: Webserver

Tomcat is an application server.

### 1. Install Java first

- To install Java
```bash
sudo yum -y install java
java -version
```
- Remove old version JDK(optional)
```bash
yum -y remove (version)
```
- Check version
```bash
java -version
```


### 2. Set JAVA_HOME Variable Path

```bash
cd /usr/lib/jvm/java-11<tab>
```
```bash
pwd 
```
copy displayed path

```bash 
vi /root/.bash_profile
```
Add the following lines to .bash_profile:
```bash
JAVA_HOME=(paste the copied path)
PATH=$PATH:$HOME/bin:$JAVA_HOME
```
Then refresh the profile:
```bash
. /root/.bash_profile

# OR

source /root/.bash_profile 
```
### 3. Download Apache Tomcat in the Form of .tar.gz and Extract It

- make a new dir opt
```bash
mkdir /opt
cd /opt
```
- Download and extract Apache Tomcat

goto the Apache Tomcat official site and copy .tar.gz link

```bash
wget <paste the copied link>
```
```bash
tar -zxvf <downloaded file>.tar.gz
```
```bash
cd /opt/apache-<tab>/bin
```
```bash
ln -s /opt/apache-tomcat<tab>/bin/startup.sh /usr/local/bin/tomcatup
ln -s /opt/apache-tomcat<tab>/bin/shutdown.sh /usr/local/bin/tomcatdown
```
```bash
echo $?  #zero indicates success
```
### 4. Change the Port of Tomcat Server (eg:8090)

```bash
cd /opt/apache-tomcat<tab>/conf
vi server.xml
```
Search for connector port, and modify it to 8090.

### 5. Allow the 8090 Port in the Firewall

```bash
firewall-cmd --permanent --add-port=8090/tcp
firewall-cmd --reload
firewall-cmd --list-all
```
### 6. Allow Access to the Tomcat Server from Any/Remote Hosts

```bash
cd /opt/apache-tomcat<tab>/webapps/host-manager/META-INF
vi context.xml
```
Search for Valve and comment it using <!-- ... -->.

again goto 
```bash
cd /opt/apache-tomcat<tab>/webapps/manager/META-INF
vi context.xml
```
Search for Valve and comment it using <!-- ... -->.

Open a browser locally or remotely to test the Apache Tomcat server: URL: http://your-ip-address:8090

### 7. Setup Credentials to Login into 'Manager App'
```bash
cd /opt/apache-tomcat<tab>/conf
vi tomcat-users.xml
```
Add the following lines to tomcat-users.xml:

```bash
<role rolename="Manager-gui"/>
<role rolename="Manager-script"/>
<role rolename="Manager-jmx"/>
<role rolename="Manager-status"/>

<user username="tomcat" password="tomcat123" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
<user username="deployer" password="deployer123" roles="manager-script"/>
```
Save and exit.

### 8. Refresh the Changes
```bash
tomcatdown
tomcatup
```
Now, the Tomcat server is installed and configured on your webserver. You can access the manager app with the provided credentials.
