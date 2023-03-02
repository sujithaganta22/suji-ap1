pipeline {
    agent any

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
                        sh "scp -o StrictHostKeyChecking=no  target/*.war ec2-user@172.31.29.121:/opt/tomcat9/webapps/ "
                        sh "ssh ec2-user@172.31.29.121 /opt/tomcat9/bin/shutdown.sh"
                        sh "ssh ec2-user@172.31.29.121 /opt/tomcat9/bin/startup.sh" 
                    }
                }
            }
            
    }
}
