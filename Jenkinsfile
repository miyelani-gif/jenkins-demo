pipeline {
    agent {
        kubernetes {
            yaml """
apiVersion: v1
kind: Pod
spec:
  serviceAccountName: default
  containers:
  - name: kubectl
    image: bitnami/kubectl:latest
    command:
    - cat
    tty: true
  - name: jnlp
    image: jenkins/inbound-agent:latest
"""
        }
    }

    stages {
        stage('Deploy to K8s') {
            steps {
                container('kubectl') {
                    sh 'kubectl get pods'
                    sh 'kubectl apply -f k8s/deployment.yaml'
                    sh 'kubectl apply -f k8s/service.yaml'
                }
            }
        }
    }
}