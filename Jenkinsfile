
pipeline {
    agent any 

    options {
        timestamps()
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
                bat "docker run -d --name shopflow-test-container -p 5000:5000 shopflow-test:${env.BUILD_NUMBER}"
            }
        }
     }

     post {
        always{
            junit 'test-reports.xml'
            cleanWs()
        }
     }
}