pipeline {
    agent any
 
    environment {
        STACK_NAME = 'naga200-com'
        TRAEFIK_PUBLIC_NETWORK = 'traefik-public'
        TRAEFIK_PUBLIC_TAG = 'traefik-public'
        TRAEFIK_TAG = 'naga200.com'
 
        DOCKER_IMAGE_BACKEND = 'backend'
        DOCKER_IMAGE_CELERYWORKER = 'celeryworker'
        DOCKER_IMAGE_FRONTEND = 'frontend'
 
        DOMAIN = 'localhost'
        SMTP_HOST = ''
        TAG = 'latest'
    }
 
    stages {
 
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
 
        stage('Create .env') {
            steps {
                sh '''
                    cat > .env <<EOF
DOMAIN=${DOMAIN}
STACK_NAME=${STACK_NAME}
TRAEFIK_PUBLIC_NETWORK=${TRAEFIK_PUBLIC_NETWORK}
TRAEFIK_PUBLIC_TAG=${TRAEFIK_PUBLIC_TAG}
TRAEFIK_TAG=${TRAEFIK_TAG}
 
DOCKER_IMAGE_BACKEND=${DOCKER_IMAGE_BACKEND}
DOCKER_IMAGE_CELERYWORKER=${DOCKER_IMAGE_CELERYWORKER}
DOCKER_IMAGE_FRONTEND=${DOCKER_IMAGE_FRONTEND}
 
SMTP_HOST=
SMTP_USER=
SMTP_PASSWORD=
SMTP_PORT=587
SMTP_TLS=True
 
BACKEND_APP_MODULE=app.main:app
BACKEND_PRE_START_PATH=/app/prestart.sh
BACKEND_PROCESS_MANAGER=uvicorn
BACKEND_WITH_RELOAD=true
INSTALL_DEV=true
INSTALL_JUPYTER=true
 
PROJECT_NAME=Naga200
SECRET_KEY=changethis
FIRST_SUPERUSER=admin@naga200.com
FIRST_SUPERUSER_PASSWORD=changethis
USERS_OPEN_REGISTRATION=True
 
MONGO_DATABASE=app
MONGO_DATABASE_URI=mongodb
 
FLOWER_BASIC_AUTH=admin:changethis
SENTRY_DSN=
 
EMAILS_FROM_EMAIL=info@naga200.com
EMAILS_FROM_NAME=Symona Adaro
EMAILS_TO_EMAIL=info@naga200.com
EOF
                '''
            }
        }
 
        stage('Docker Config Check') {
            steps {
                sh 'docker compose config'
            }
        }
 
        stage('Docker Build') {
            steps {
                sh 'docker compose build'
            }
        }
 
        stage('Deploy') {
            steps {
                sh 'docker compose up -d'
            }
        }
 
        stage('Verify') {
            steps {
                sh 'docker compose ps'
            }
        }
    }
}
