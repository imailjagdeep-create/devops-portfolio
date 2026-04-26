# DevOps Portfolio Website

## Run with Docker
\`\`\`bash
docker build -t my-portfolio .
docker run -d -p 8081:80 my-portfolio
\`\`\`

## Deploy to Kubernetes
\`\`\`bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
\`\`\`

## Access
- Local: http://localhost:8081
- Kubernetes: http://localhost:30080