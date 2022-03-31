pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            git credentialsId: 'GITHUB_CREDENTIALS', url: 'https://github.com/ashutoshkrris-tw/to-do-app'
        }

        stage('Docker Build Image') {
            steps {
                sh 'docker version'
                sh 'docker build -t ashutoshkrris/kanban-board-app:v1.0 .'
                sh 'docker images'
            }
        }

        withCredentials([string(credentialsId: 'DOCKERHUB_PASSWORD', variable: 'PASSWORD')]) {
            sh 'docker login -u ashutoshkrris -p $PASSWORD'
        }

        stage('Push Image to DockerHub') {
            steps {
                sh 'docker push  ashutoshkrris/kanban-board-app:1.0'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'kubectl apply -f board.yaml'
            }
        }
    }
}
