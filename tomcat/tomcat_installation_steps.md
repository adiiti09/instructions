https://www.digitalocean.com/community/tutorials/how-to-install-apache-tomcat-10-on-ubuntu-20-04

# Tomcat installation ob Ubuntu 22.04
## Create tomcat user along with home directory
## For security purposes, Tomcat should run under a separate, unprivileged user
      sudo useradd -m -U -d /opt/tomcat -s /bin/false tomcat

## Check and install JDK if needed
      sudo apt install openjdk-11-jdk

## Set version to download the binaries
      VERSION=10.1.16
      wget https://downloads.apache.org/tomcat/tomcat-10/v${VERSION}/bin/apache-tomcat-${VERSION}.tar.gz

## Extract to the installation directory created above
      sudo tar -xf apache-tomcat-${VERSION}.tar.gz -C /opt/tomcat/

## Create a softlink to the installation folder as latest
      sudo ln -s /opt/tomcat/apache-tomcat-${VERSION} /opt/tomcat/latest

## Change ownership and give required executable access to tomcat
      sudo chown -R tomcat:tomcat /opt/tomcat/
      sudo chmod -R u+x /opt/tomcat/latest/bin

# Config admin users
## We need to define privileged users in Tomcat’s configuration for accessing through UI

      sudo nano /opt/tomcat/latest/conf/tomcat-users.xml

## At the bottom add the below lines, just above the closing tag

      <role rolename="manager-gui" />
      <user username="manager" password="manager_password" roles="manager-gui" />

      <role rolename="admin-gui" />
      <user username="admin" password="admin_password" roles="manager-gui,admin-gui" />

## To remove the restriction for the Manager page, open its config file for editing
      sudo nano /opt/tomcat/latest/webapps/manager/META-INF/context.xml

## Comment out the Valve definition, as shown

      ...
      <Context antiResourceLocking="false" privileged="true" >
      <CookieProcessor className="org.apache.tomcat.util.http.Rfc6265CookieProcessor"
                   sameSiteCookies="strict" />
      <!--  <Valve className="org.apache.catalina.valves.RemoteAddrValve"
               allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->
      <Manager sessionAttributeValueClassNameFilter="java\.lang\.(?:Boolean|Integer|Long|Number|String)|org\.apache\.catalina\.filters\.Csr>
      </Context>

## Repeat the same for host manager as well by editing the below file
      sudo nano /opt/tomcat/latest/webapps/host-manager/META-INF/context.xml

# Creating a `systemd` service
## We can create a systemd service to start, stop, restart tomcat and enable it to keep running in the background
## Get the java location using the below command and make a note of it

      sudo update-java-alternatives -l

## Create the service file
      sudo nano /etc/systemd/system/tomcat.service

## Paste the below text ensuring to replace values with actual values applicable to your system

      [Unit]
      Description=Tomcat
      After=network.target

      [Service]
      Type=forking

      User=tomcat
      Group=tomcat

      Environment="JAVA_HOME=/usr/lib/jvm/java-1.11.0-openjdk-amd64" # change this as appropriate
      Environment="JAVA_OPTS=-Djava.security.egd=file:///dev/urandom"
      # Ensure that the installation location is correct
      Environment="CATALINA_BASE=/opt/tomcat/latest"
      Environment="CATALINA_HOME=/opt/tomcat/latest"
      Environment="CATALINA_PID=/opt/tomcat/latest/temp/tomcat.pid"
      Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"

      ExecStart=/opt/tomcat/latest/bin/startup.sh
      ExecStop=/opt/tomcat/latest/bin/shutdown.sh

      RestartSec=10
      Restart=always

      [Install]
      WantedBy=multi-user.target

## Reload the systemd daemon so that it becomes aware of the new service
      sudo systemctl daemon-reload

## Start, stop restart, check status of tomcat using
      sudo systemctl start tomcat
      sudo systemctl stop tomcat
      sudo systemctl restart tomcat
      sudo systemctl status tomcat

## To enable Tomcat starting up with the system use
      sudo systemctl enable tomcat

# Accessing the web interface
## Tomcat uses port 8080 to accept HTTP requests

### local - sudo ufw allow 8080/tcp
### Azure VM - Add inbound rule

## In case of any other applocation running already on port 8080 causing tomcat start to fail
## Go to /opt/tomcat/latest/conf
         sudo nano /opt/tomcat/latest/conf/server.xml
         #Find 8080 and change it to 8088 or some free port

## Restart the service
## Open http://<server_ip>:8088
