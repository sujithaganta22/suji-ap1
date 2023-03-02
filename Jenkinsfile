pipeline {
    agent any
    environment {
  TOMCAT_DEV = "172.31.29.121"
  TOMCAT_USER = "ec2-user"
}
    parameters {
  string defaultValue: 'main', description: 'chose branch to build and deploy', name: 'branchname'
}

 stages {
        stage('Git Checkout') {
            when {
                expression{
                params.branchname == "develop"
                }
            }
             steps {
                git branch: "${params.branchname}", credentialsId: 'github', url: 'https://github.com/sujithaganta22/suji-ap1'
            } 
        }    
            stage('Maven Build') {
                 when {
                     expression{
                params.branchname == "develop"
            }
                 }
                steps {
                   sh 'mvn clean package'
            
                }
            }
            stage("Dev Deploy"){
                 when {
                     expression{
                params.branchname == "develop"
            }
                 }
                steps{
                    sshagent(['tomcat-dev']) {
                        // copy war file ontpo tomcat server
                        sh "scp -o StrictHostKeyChecking=no target/*.war $TOMCAT_USER@$TOMCAT_DEV:/opt/tomcat9/webapps/ "
                        sh "ssh $TOMCAT_USER@$TOMCAT_DEV /opt/tomcat9/bin/shutdown.sh"
                        sh "ssh $TOMCAT_USER@$TOMCAT_DEV /opt/tomcat9/bin/startup.sh" 
                    }
                }
            }
            
    }
    post {
  success {
      echo "job successed,sending sucess email"
  }
  failure {
    echo "job failed, sending failure email"
  }
}

}
