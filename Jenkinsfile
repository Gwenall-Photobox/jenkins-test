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
                checkout scm
                def is_pr = env.JOB_NAME.endsWith("_pull-requests");
    setGitHubPullRequestStatus state: 'PENDING', context: "${env.JOB_NAME}", message: "Run #${env.BUILD_NUMBER} started";

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
