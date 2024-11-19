pipeline {
    agent any

    environment {
        kubeConfig = credentials('kubeconfig')
    }

    stages {
        stage('Checkout Code') {
            steps {
                 git branch: 'main', url: 'https://github.com/Putumerta-collab/mysql_deployment.git'
            }
        }

        stage('Deploy PHP App to Kubernetes') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG')]) {
                    sh '''
               
                    kubectl --kubeconfig=$KUBECONFIG apply -f mysql-service.yaml
                    '''
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
