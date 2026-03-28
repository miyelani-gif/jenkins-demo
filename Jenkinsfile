pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/mayayisim/jenkins-demo.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying app...'
            }
        }
    }
}