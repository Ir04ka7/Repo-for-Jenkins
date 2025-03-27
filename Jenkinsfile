pipeline {
    agent any

    environment {
        JENKINS_URL = "${env.JENKINS_URL}"
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
