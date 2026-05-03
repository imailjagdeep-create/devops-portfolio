# DevOps Portfolio Website
A modern, responsive portfolio website for a DevOps Engineer, containerized with Docker and deployed on Kubernetes with a fully automated CI/CD pipeline.


### Key Features:
- Responsive portfolio website with modern design
- Containerized using Docker with lightweight Alpine base image
- Automated CI/CD pipeline using Jenkins (4 stages)
- Orchestrated on Kubernetes with high availability
- Version controlled using Git with proper branching strategy



##  Technologies Used

| Category | Technologies | Version |
|----------|--------------|---------|
| **Frontend** | HTML5, CSS3, Google Fonts | - |
| **Containerization** | Docker, Nginx Alpine | Docker 29.04 |
| **Orchestration** | Kubernetes | K8s 1.28.0 |
| **CI/CD** | Jenkins Pipeline | Jenkins 2.440.3 |
| **Version Control** | Git, GitHub | Git 2.21.0 |
| **Web Server** | Nginx | Alpine Linux |


## Prerequisites for Local Setup

Before running this project, ensure you have the following installed:

| Software | Minimum Version | Purpose |
|----------|----------------|---------|
| **Git** | 2.21+ | Version control |
| **Docker** | 24.0+ | Containerization |
| **Kubernetes** | 1.28+ | Orchestration |
| **Java** | 17+ | Jenkins runtime |
| **Jenkins** | 2.440+ | CI/CD pipeline |

### Verify Installations:
git --version
docker --version
kubectl version --client
java -version

### Docker Commands
# Build the image
docker build -t jagdeep1122/my-portfolio:latest .

# Run the container (port 8081)
docker run -d -p 8081:80 jagdeep1122/my-portfolio:latest

# Verify running container
docker ps

# Push to Docker Hub
docker push jagdeep1122/my-portfolio:latest

### Kubernetes Commands
bash
# Deploy application
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

# Check status
kubectl get pods          # Should show 2 running pods
kubectl get services      # Should show NodePort

# Access application
kubectl port-forward service/portfolio-service 31181:80

# Open browser to: http://localhost:31181

# Rolling update test
kubectl set image deployment/portfolio-deployment portfolio=jagdeep1122/my-portfolio:v1
kubectl rollout status deployment/portfolio-deployment

# Delete deployment
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml

### Start Jenkins
java -jar jenkins.war --httpPort=8081

# Access Jenkins: http://localhost:8081

devops-portfolio/
│
├── index.html                 # Main portfolio webpage
├── style.css                  # CSS stylesheet
├── Dockerfile                 # Docker configuration
├── deployment.yaml            # Kubernetes deployment (2 replicas, rolling updates)
├── service.yaml               # Kubernetes service (NodePort)
├── Jenkinsfile                # Jenkins CI/CD pipeline (4 stages)
├── .gitignore                 # Git ignore rules
├── README.md                  # Project documentation
│
└── images/
    └── devops.jpg             # Profile image

Name: Jagdeep Singh
Role: DevOps Engineer