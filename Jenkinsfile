pipeline {
    agent any
    stages {
        stage("Check tools") {
            steps {
                sh '''
                docker version
                docker compose version
                curl --version
                '''    
            }
        }
        stage("Prune docker") {
            steps {
                sh 'docker system prune -a --volumes -f'
            }
        }
        stage("Build") {
            steps {
                sh 'docker-compose build'
            }
        }
        stage("Run") {
            steps {
                sh 'docker-compose up -d --no-color --wait'
                sh 'docker-compose ps'
            }
        }
        stage("Test") {
            steps {
                sh 'curl http://localhost:3000'
            }
        }
    }
    post {
        always {
            sh 'docker-compose down --remove-orphans -v'
            sh 'docker-compose ps'
        }
    }
}