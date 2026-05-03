pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'jagdeep1122/my-portfolio'
        DOCKER_TAG = 'latest'
        DOCKER_PATH = 'C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe'
    }
    
    stages {
        stage('Code Pull') {
            steps {
                echo '========================================='
                echo 'STAGE 1: Pulling code from GitHub...'
                echo '========================================='
                git branch: 'main', 
                    url: 'https://github.com/imailjagdeep-create/devops-portfolio.git'
                echo 'Code pulled successfully!'
            }
        }
        
        stage('Image Build') {
            steps {
                echo '========================================='
                echo 'STAGE 2: Building Docker image...'
                echo '========================================='
                bat "\"${env.DOCKER_PATH}\" build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                echo 'Docker image built!'
            }
        }
        
        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    // Use -p flag directly instead of --password-stdin (safer on Windows)
                    bat "\"${env.DOCKER_PATH}\" login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%"
                    bat "\"${env.DOCKER_PATH}\" push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
                echo 'Image pushed to Docker Hub!'
            }
        }
        
        stage('Deploy') {
            steps {
                echo '========================================='
                echo 'STAGE 4: Deploying to Kubernetes...'
                echo '========================================='
                bat "kubectl apply -f deployment.yml"
                bat "kubectl apply -f service.yml"
                bat "kubectl rollout status deployment/portfolio-deployment"
                echo 'Deployment complete!'
            }
        }
    }
    
    post {
        success {
            echo 'PIPELINE EXECUTED SUCCESSFULLY!'
            echo 'Application URL: http://localhost:31181'
        }
        failure {
            echo 'PIPELINE FAILED!'
        }
    }
}