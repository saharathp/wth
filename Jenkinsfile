pipeline {
    agent any
    
    tools {nodejs "node 14"}

    // environment {
    //     DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials') 
    // }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                dir('all_in_docker/client') {
                script {
                        sh 'npm install'
                }
            }
            }
        }
        stage('Build') {
            steps {
                dir('all_in_docker/client') {
                    script {
                        sh 'CI=false npm run build'
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs() 
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
