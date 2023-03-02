pipeline {
    agent any
    environment {
  tomcat-dev = "172.31.29.121"
  tomcat-user = "ec2-user"
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
                        sh "scp -o StrictHostKeyChecking=no  target/*.war $tomcat-user@$tomcat-dev:/opt/tomcat9/webapps/ "
                        sh "ssh $tomcat-user@$tomcat-dev /opt/tomcat9/bin/shutdown.sh"
                        sh "ssh $tomcat-user@$tomcat-dev /opt/tomcat9/bin/startup.sh" 
                    }
                }
            }
            
    }
}
