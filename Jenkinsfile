pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t ashutoshkrris/kanban-board:latest .'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push ashutoshkrris/kanban-board:latest'
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f board.yaml'
                sh 'minikube service --url kanban-board-service'
                sh 'kubectl get pods'
            }
        }
    }
    post {
        always {
          sh 'rm -rf to-do-app'
        }
  }
}
