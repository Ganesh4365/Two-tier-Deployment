pipeline {
    agent any
    stages {
        stage('Clone repo's') {
            steps {
                git branch: 'main', url: 'https://github.com/Ganesh4365/Two-tier-Deployment.git'
            }
        }
        stage('Deploy with Docker Compose') {
            steps {
                // Use --quiet to keep logs clean, but --build to ensure fresh code
                sh 'docker compose down --remove-orphans || true'
                sh 'docker compose up -d --build'
            }
        }
        stage('Verify Deployment') {
            steps {
                // This will show you exactly what happened in the Jenkins console
                sh 'docker ps'
                sh 'sleep 10' // Give Flask a moment to start after MySQL healthcheck
                sh 'docker logs two-tier-app'
            }
        }
    }
}
