pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
 
        stage('Docker Build') {
            steps {
                sh '''
                    export TRAEFIK_PUBLIC_NETWORK=traefik-public
                    docker compose build
                '''
            }
        }
 
        stage('Deploy') {
            steps {
                sh '''
                    export TRAEFIK_PUBLIC_NETWORK=traefik-public
                    docker compose up -d
                '''
            }
        }
 
        stage('Verify') {
            steps {
                sh 'docker compose ps'
            }
        }
    }
}
