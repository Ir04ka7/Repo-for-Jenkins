pipeline {
    agent any
    stages {
        stage('Prepare') {
            steps {
                script {
                    sh 'curl -fsSL https://deb.nodesource.com/setup_22.x | bash -'
                    sh 'sudo apt install -y nodejs'
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'npm --version'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'echo "JENKINS_URL=$JENKINS_URL"'
                }
            }
        }
    }
}
