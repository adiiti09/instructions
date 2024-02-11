# Create tomcat user along with home directory
## For security purposes, Tomcat should run under a separate, unprivileged user
      sudo useradd -m -U -d /opt/tomcat -s /bin/false tomcat

2. VERSION=10.1.16
   wget https://downloads.apache.org/tomcat/tomcat-10/v${VERSION}/bin/apache-tomcat-${VERSION}.tar.gz

3. sudo tar -xf apache-tomcat-${VERSION}.tar.gz -C /opt/tomcat/

4. sudo ln -s /opt/tomcat/apache-tomcat-${VERSION} /opt/tomcat/latest

5. sudo chown -R tomcat: /opt/tomcat

6. sudo sh -c 'chmod +x /opt/tomcat/latest/bin/*.sh'

7. sudo nano /etc/systemd/system/tomcat.service

/etc/systemd/system/tomcat.service
[Unit]
Description=Tomcat 10 servlet container
After=network.target
[Service]
Type=forking
User=tomcat
Group=tomcat
Environment="JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64"
Environment="JAVA_OPTS=-Djava.security.egd=file:///dev/urandom -Djava.awt.headless=true"
Environment="CATALINA_BASE=/opt/tomcat/latest"
Environment="CATALINA_HOME=/opt/tomcat/latest"
Environment="CATALINA_PID=/opt/tomcat/latest/temp/tomcat.pid"
Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"
ExecStart=/opt/tomcat/latest/bin/startup.sh
ExecStop=/opt/tomcat/latest/bin/shutdown.sh
[Install]
WantedBy=multi-user.target


8. sudo systemctl daemon-reload

sudo systemctl enable --now tomcat

sudo systemctl status tomcat


sudo systemctl start tomcat
sudo systemctl stop tomcat
sudo systemctl restart tomcat


local - sudo ufw allow 8080/tcp
Azure VM - Add inbound rule

Go to /opt/tomcat/latest/conf
sudo /opt/tomcat/latest/conf/nano server.xml
Find 8080 abd change it to 8088

Start the service

Add inbound rule for port 8088

Open http://<server_ip>:8088
