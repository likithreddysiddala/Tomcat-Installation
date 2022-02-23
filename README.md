# Tomcat-Installation

# sudo wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.58/bin/apache-tomcat-9.0.58.tar.gz
# sudo tar -xvzf apache-tomcat-9.0.58
# sudo chown -R ec2-user:ec2-user apache-tomcat-9.0.58
Start tomcat:
# cd /apache-tomcat-10.0.16-src/bin

# ./startup.sh

(connecting outside world to edit context.xml) 
 search for context.xml
# find / -name context.xml


you will get three files 

/home/ec2-user/apache-tomcat-9.0.58/webapps/host-manager/META-INF/context.xml
/home/ec2-user/apache-tomcat-9.0.58/webapps/manager/META-INF/context.xml

vi /home/ec2-user/apache-tomcat-9.0.58/webapps/host-manager/META-INF/context.xml
vi /home/ec2-user/apache-tomcat-9.0.58/webapps/manager/META-INF/context.xml

# add <!--       ending -->
<!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"
  allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />  -->

After that restart tomcat services to effect these changes

# ./shutdown.sh
# ./startup.sh
User & Password Edit:
# cd ../
# cd conf
# vi tomcat-users.xml
 add user details :
	<role rolename="manager-gui"/>
	<role rolename="manager-script"/>
	<role rolename="manager-jmx"/>
	<role rolename="manager-status"/>
	<user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
	<user username="deployer" password="deployer" roles="manager-script"/>
	<user username="tomcat" password="s3cret" roles="manager-gui"/>
((((((EXAMPLE))))))))))
-->
  <role rolename="manager-gui"/>
        <role rolename="manager-script"/>
        <role rolename="manager-jmx"/>
        <role rolename="manager-status"/>
        <user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
        <user username="deployer" password="deployer" roles="manager-script"/>
        <user username="tomcat" password="s3cret" roles="manager-gui"/>
  </tomcat-users>
(((((((EXAMPLE)))))))))))

If you want to change tomcat port number:
# cd conf/
# vi server.xml

Edit section under Connector port 8080 to 8090 (ur wish)

To start Tomcat:
# ./startup.sh

Jenkins to Tomcat integration:

--> Install deploy to container plugin
--> Under post build action -> deploy war or ear container 
--> **/*.war
   add tomcat user details 
   apply & save
