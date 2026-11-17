
pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'Source code downloaded'
            }
        }

        stage('Check Git') {
            steps {
                sh 'git --version'
                sh 'git log -1 --oneline'
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                    docker build \
                      -t react-nginx-app:${BUILD_NUMBER} .
                '''
            }
        }

        stage('Verify Image') {
            steps {
                sh '''
                    docker image inspect \
                      react-nginx-app:${BUILD_NUMBER}
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
