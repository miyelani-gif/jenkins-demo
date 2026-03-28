pipeline {
    agent {
        kubernetes {
            yaml """
apiVersion: v1
kind: Pod
spec:
  serviceAccountName: default
  containers:
  - name: kaniko
    image: gcr.io/kaniko-project/executor:latest
    command:
    - sleep
    args:
    - "9999999"
    tty: true
    volumeMounts:
    - name: docker-config
      mountPath: /kaniko/.docker
  - name: kubectl
    image: lachlanevenson/k8s-kubectl:latest
    command:
    - cat
    tty: true
  - name: jnlp
    image: jenkins/inbound-agent:latest
  volumes:
  - name: docker-config
    secret:
      secretName: dockerhub-secret
"""
        }
    }

    environment {
        IMAGE_NAME = "miyelani/jenkins-demo:latest"
    }

    stages {

        stage('Build & Push Image') {
            steps {
                container('kaniko') {
                    sh """
                    /kaniko/executor \
                      --dockerfile=Dockerfile \
                      --context=. \
                      --destination=$IMAGE_NAME \
                      --skip-tls-verify
                    """
                }
            }
        }

        stage('Deploy to K8s') {
            steps {
                container('kubectl') {
                    sh '''
                      kubectl apply -f k8s/deployment.yaml
                      kubectl apply -f k8s/service.yaml
                    '''
                }
            }
        }
    }
}