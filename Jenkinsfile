pipeline {
    agent any

    environment {
        JENKINS_URL = "http://192.168.0.193:8080/"
    }

    stages {
        stage('Prepare') {
            steps {
                sh 'node -v'
            }
        }

        stage('Build') {
            steps {
                sh 'npm --version'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "JENKINS_URL=$JENKINS_URL"'
            }
        }
    }
}
