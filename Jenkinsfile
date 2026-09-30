
pipeline {
    agent any 

    options {
        timestamps()
    }

    environment {
        container = 'shopflow-app-container'
    }

     stages {
        stage('Install') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                bat 'python -m pytest --junitxml=test-reports.xml'
            }
        }

        stage('docker build') {
            steps {
                bat "docker build -t shopflow-test:${env.BUILD_NUMBER} ."
            }
        }

        stage('Run build') {
            steps {
                bat "docker run -d --name %container% -p 5000:5000 shopflow-test:${env.BUILD_NUMBER}"
            }
        }

        stage('smkoe test') {
            steps {
                sleep 5
                bat 'curl -f http://localhost:5000/health'
            }
        }
     }

     post {
        always{
            junit 'test-reports.xml'
            bat 'docker rm -f %container% || exit 0'
            cleanWs()
        }
     }
}