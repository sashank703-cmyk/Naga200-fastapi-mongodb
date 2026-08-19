pipeline {
    agent any
 
    environment {
        STACK_NAME = 'naga200-com'
        TRAEFIK_PUBLIC_NETWORK = 'traefik-public'
        TRAEFIK_PUBLIC_TAG = 'traefik-public'
        TRAEFIK_TAG = 'naga200.com'
    }
 
    stages {
 
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
 
        stage('Docker Build') {
            steps {
                sh '''
                    docker compose build
                '''
            }
        }
 
        stage('Deploy') {
            steps {
                sh '''
                    docker compose up -d
                '''
            }
        }
 
        stage('Verify') {
            steps {
                sh '''
                    docker compose ps
                '''
            }
        }
    }
}
 
