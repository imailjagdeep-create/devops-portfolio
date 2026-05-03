# DevOps Portfolio Website

A modern, responsive portfolio website for a DevOps Engineer, containerized with Docker and deployed on Kubernetes with a fully automated CI/CD pipeline.

## Quick Start

### Prerequisites
- Docker
- Kubernetes (Minikube or Docker Desktop)
- Git
- Jenkins (optional, for CI/CD)

### Run with Docker
docker build -t jagdeep1122/my-portfolio:latest .
docker run -d -p 8081:80 jagdeep1122/my-portfolio:latest

## Run with Docker
docker build -t my-portfolio .
docker run -d -p 8081:80 my-portfolio

## Deploy to Kubernetes
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

## Access
- Local: http://localhost:8081
- Kubernetes: http://localhost:30080
