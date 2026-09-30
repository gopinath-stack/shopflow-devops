pipeline {
    agent any 
    stages {
        stage('Install') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                bat 'python -m pytest --junitxml=test-report.xml'
            }
        }
    }

    post {
        always {
            junit 'test-reports.xml'
        }
    }
}