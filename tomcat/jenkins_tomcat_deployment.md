# Deployment stage of Jenkins CI/CD pipeline script

        stage ('Deploy') {

            steps {
                echo "deploy stage"
                deploy adapters: [tomcat9 (
                        credentialsId: 'tomcat_deploy_credentials',
                        path: '',
                        url: 'http://52.172.90.142:8080/'
                    )],
                    contextPath: 'test',
                    onFailure: 'false',
                    war: '**/*.war'
            }
        }

# Set up to be done on the tomcat side

- Edit <tomcat_home>/conf/tomcat-users.xml
- Add the followoing lines:
    - /<role rolename="manager-script"/>
    - /<user username="<some_username>" password="<some_password>" roles="manager-script"/>
- In Jenkins, create a credentials entry with the above username and password with some like **tomcat_deploy_credentials**
- Use that ID in the above script against the element **credentialsId**.
- Replace the host and port in the above URL with the host and port of your tomcat instance
- Choose an appropriate context path. This is the name with which the deployment can be accessed from the URL like "**<tomcat_host>:/<port>/<context_path>**"
