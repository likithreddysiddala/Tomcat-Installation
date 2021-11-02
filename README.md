# Tomcat-Installation

# sudo wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.54/bin/apache-tomcat-9.0.54.tar.gz
# sudo tar -xvzf apache-tomcat-9.0.54
# sudo chown -R ec2-user:ec2-user apache-tomcat-9.0.54
Start tomcat:
# cd /apache-tomcat-9.0.54/bin

(connecting outside world to edit context.xml) 
 search for context.xml
# find / -name context.xml

<!--
  -->
above command gives 3 context.xml files.             
comment () Value ClassName field on files which are under webapp directory.
After that restart tomcat services to effect these changes

# ./shutdown.sh
# ./startup.sh
User & Password Edit:
# cd ../
# cd conf
# vi user-server.xml
 add user details :
	<role rolename="manager-gui"/>
	<role rolename="manager-script"/>
	<role rolename="manager-jmx"/>
	<role rolename="manager-status"/>
	<user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
	<user username="deployer" password="deployer" roles="manager-script"/>
	<user username="tomcat" password="s3cret" roles="manager-gui"/>

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
