pipeline {
    agent any

    environment {
        JENKINS_URL = "http://192.168.0.193:8080/"
    }

    stages {
        stage('Prepare') {
            steps {
                sh '''
                    curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
                    sudo apt install -y nodejs
                '''
            }
        }

        stage('Build') {
            steps {
                sh 'npm -v'
            }
        }

        stage('Test') {
            steps {
                sh 'echo JENKINS_URL: $JENKINS_URL'
            }
        }
    }
}
