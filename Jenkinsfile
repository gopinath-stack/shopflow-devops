pipeline {
    agent any 
    stages {
        stage('Install') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }
    }
}