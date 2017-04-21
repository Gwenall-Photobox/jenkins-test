pipeline {
    agent any 

    stages {
        stage('Build') { 
             post {
                failure {
                    echo 'HERE'
                }
              }
            steps { 
                githubNotify description: 'This is a shorted example',  status: 'SUCCESS'
                sh 'make' 
            }
        }
        stage('Test'){
            steps {
                sh 'make check'
                junit 'reports/**/*.xml' 
            }
        }
        stage('Deploy') {
            steps {
                sh 'make publish'
            }
        }
    }
}
