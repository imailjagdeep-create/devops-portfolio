pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'jagdeep1122/my-portfolio'
        DOCKER_TAG = 'latest'
        DOCKER_PATH = 'C:\\Program Files\\Docker\\Docker\\frontend\\docker.exe'
    }
    
    stages {
        // Stage 1: Pull code from Git
        stage('Code Pull') {
            steps {
                echo '========================================='
                echo '📦 STAGE 1: Pulling code from GitHub...'
                echo '========================================='
                git branch: 'main', 
                    url: 'https://github.com/imailjagdeep-create/devops-portfolio.git'
                echo '✅ Code pulled successfully!'
            }
        }
        
        // Stage 2: Build Docker image
        stage('Image Build') {
            steps {
                echo '========================================='
                echo '🐳 STAGE 2: Building Docker image...'
                echo '========================================='
                bat "\"${DOCKER_PATH}\" build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                echo '✅ Docker image built!'
            }
        }
        
        // Stage 3: Push image to registry
        stage('Push Image') {
            steps {
                echo '========================================='
                echo '📤 STAGE 3: Pushing image to Docker Hub...'
                echo '========================================='
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub', 
                    passwordVariable: 'DOCKER_PASSWORD', 
                    usernameVariable: 'DOCKER_USERNAME'
                )]) {
                    bat "echo %DOCKER_PASSWORD% | \"${DOCKER_PATH}\" login -u %DOCKER_USERNAME% --password-stdin"
                    bat "\"${DOCKER_PATH}\" push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
                echo '✅ Image pushed to Docker Hub!'
            }
        }
        
        // Stage 4: Deploy to Kubernetes
        stage('Deploy') {
            steps {
                echo '========================================='
                echo '☸️ STAGE 4: Deploying to Kubernetes...'
                echo '========================================='
                bat "kubectl apply -f deployment.yaml"
                bat "kubectl apply -f service.yaml"
                bat "kubectl rollout status deployment/portfolio-deployment"
                echo '✅ Deployment complete!'
            }
        }
    }
    
    post {
        success {
            echo '========================================='
            echo '🎉 PIPELINE EXECUTED SUCCESSFULLY! 🎉'
            echo '========================================='
            echo '📍 Application URL: http://localhost:30080'
            echo '========================================='
        }
        failure {
            echo '========================================='
            echo '❌ PIPELINE FAILED!'
            echo '========================================='
            echo 'Check the logs above for errors.'
            echo 'Common issues:'
            echo '  - Docker Desktop not running'
            echo '  - Kubernetes not enabled in Docker Desktop'
            echo '  - Docker Hub credentials incorrect'
            echo '========================================='
        }
    }
}