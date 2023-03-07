pipeline {
    agent any

    stages {
        stage('Maven Build') {
            when {
                branch 'develop'
            }
            steps {
                echo 'Hello World'
            }
        }
        stage('Dev Deploy') {
             when {
                branch 'develop'
            }
            steps {
                echo 'Hello World'
            }
        }
      stage('Test Deploy') {
           when {
                branch 'test'
            }
            steps {
                echo 'Hello World'
            }
        }
      stage('Uat Deploy') {
           when {
                branch 'uat'
            }
            steps {
                echo 'Hello World'
            }
        }
    }
}
