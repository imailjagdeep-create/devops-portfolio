pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'jagdeep1122/my-portfolio'
        DOCKER_TAG = 'latest'
    }
    
    stages {
        // Stage 1: Pull code from Git
        stage('Code Pull') {
            steps {
                echo 'Pulling code from GitHub...'
                git branch: 'main', 
                    url: 'https://github.com/imailjagdeep-create/devops-portfolio.git'
                echo 'Code pulled successfully!'
            }
        }
        
        // Stage 2: Build Docker image
        stage('Image Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .'
                echo 'Docker image built!'
            }
        }
        
        // Stage 3: Push image to registry
        stage('Push Image') {
            steps {
                echo 'Pushing image to Docker Hub...'
                withCredentials([usernamePassword(credentialsId: 'docker-hub', 
                                                  passwordVariable: 'DOCKER_PASSWORD', 
                                                  usernameVariable: 'DOCKER_USERNAME')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker push ${DOCKER_IMAGE}:${DOCKER_TAG}'
                }
                echo 'Image pushed to Docker Hub!'
            }
        }
        
        // Stage 4: Deploy to Kubernetes
        stage('Deploy') {
            steps {
                echo 'Deploying to Kubernetes...'
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
                sh 'kubectl rollout status deployment/portfolio-deployment'
                echo 'Deployment complete!'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline executed successfully!'
            echo 'Application URL: http://localhost:30080'
        }
        failure {
            echo 'Pipeline failed! Check logs above.'
        }
    }
}