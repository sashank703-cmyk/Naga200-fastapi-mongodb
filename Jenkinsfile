pipeline {
    agent any
 
    environment {
        TRAEFIK_PUBLIC_NETWORK = 'traefik-public'
        TRAEFIK_PUBLIC_TAG = 'traefik-public'
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
                    export TRAEFIK_PUBLIC_NETWORK=traefik-public
                    export TRAEFIK_PUBLIC_TAG=traefik-public
                    docker compose build
                '''
            }
        }
 
        stage('Deploy') {
            steps {
                sh '''
                    export TRAEFIK_PUBLIC_NETWORK=traefik-public
                    export TRAEFIK_PUBLIC_TAG=traefik-public
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
