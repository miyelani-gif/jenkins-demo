pipeline {
    agent {
        kubernetes {
            defaultContainer 'kubectl'
        }
    }

    stages {
        stage('Deploy to K8s') {
            steps {
                sh 'kubectl get nodes'
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
}
