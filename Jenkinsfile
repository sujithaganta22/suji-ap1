pipeline {
    agent any
    environment {
  TOMCAT_DEV = "172.31.29.121"
  TOMCAT_USER = "ec2-user"
}
 stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/sujithaganta22/suji-ap1'
            } 
        }    
            stage('Maven Build') {
                steps {
                   sh 'mvn clean package'
            
                }
            }
            stage("Dev Deploy"){
                steps{
                    sshagent(['tomcat-dev']) {
                        // copy war file ontpo tomcat server
                        sh "scp -o StrictHostKeyChecking=no  target/*.war $TOMCAT_USER@$TOMCAT_DEV:/opt/tomcat9/webapps/ "
                        sh "ssh $TOMCAT_USER @$TOMCAT_DEV  /opt/tomcat9/bin/shutdown.sh"
                        sh "ssh $TOMCAT_USER @$TOMCAT_DEV  /opt/tomcat9/bin/startup.sh" 
                    }
                }
            }
            
    }
}
