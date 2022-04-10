pipeline {
    agent any
    environment {
        CI = 'true'
    }
    options {
        skipDefaultCheckout(true)
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo present working dir: && pwd'
                checkout scm
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
