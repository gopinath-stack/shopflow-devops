
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
     }

     post {
        always{
            junit 'test-reports.xml'
            cleanWs()
        }
     }
}