# Deployment stage of Jenkins CI/CD pipeline script

        stage ('Deploy') {

            steps {
                echo "deploy stage"
                deploy adapters: [tomcat9 (
                        credentialsId: 'tomcat_deploy',
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
-  
