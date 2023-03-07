pipeline {
    agent any

    stages {
        stage('Maven Build') {
            when {
                branch 'develop'
            }
            steps {
                echo 'maven build'
            }
        }
        stage('Dev Deploy') {
             when {
                branch 'develop'
            }
            steps {
                echo 'dev deploy'
            }
        }
      stage('Test Deploy') {
           when {
                branch 'test'
            }
            steps {
                echo 'test deploy'
            }
        }
      stage('Uat Deploy') {
           when {
                branch 'uat'
            }
            steps {
                echo 'uat depploy'
            }
        }
    }
}
