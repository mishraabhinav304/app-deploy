pipeline {
    agent {
        kubernetes {
            cloud 'kubernetes'
            defaultContainer 'helm'
            yaml '''
apiVersion: v1
kind: Pod
metadata:
  labels:
    build: my-app
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
            - key: kubernetes.io/hostname
              operator: In
              values:
              - minikube
  containers:
    - name: helm
      image: dtzar/helm-kubectl:3.9.0
      command:
        - sleep
      args:
        - 99d
'''
        }
    }

    stages {
        stage('Helm Deploy') {
            steps {
                container('helm') {
                    sh '''
                        echo "Helm and kubectl test"
                        helm version
                        kubectl get nodes -o wide
                        kubectl get pods -A
                    '''
                }
            }
        }
    }
}
