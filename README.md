# Kubernetes NGINX Deployment Lab

## Overview

This lab demonstrates how to deploy and manage a simple NGINX web application using Kubernetes. The application will be exposed using Kubernetes services and will be deployed in a local Minikube cluster. Various Kubernetes commands and troubleshooting techniques are applied throughout the process to ensure the deployment is successful.

## Prerequisites

- **Minikube** installed
- **kubectl** CLI installed
- Docker installed and configured (for Minikube Docker driver)
- Familiarity with basic Kubernetes concepts such as Pods, Deployments, Services, and kubectl commands

## Steps Involved

### 1. **Set Up Minikube**
   - Start a Minikube cluster with the desired Kubernetes version:
     ```bash
     minikube start --kubernetes-version=v1.27.0
     ```

### 2. **Create NGINX Deployment**
   - Deploy NGINX using a deployment YAML file:
     ```bash
     kubectl apply -f nginx-deployment.yaml
     ```

### 3. **Check Deployment**
   - Verify the deployment status:
     ```bash
     kubectl get deployments
     ```

### 4. **Expose the NGINX Deployment**
   - Expose the NGINX deployment through a Kubernetes service:
     ```bash
     kubectl expose deployment nginx-deployment --type=LoadBalancer --port=80 --target-port=80
     ```

### 5. **Verify Pods and Services**
   - Verify the running pods:
     ```bash
     kubectl get pods
     ```
   - Verify the service:
     ```bash
     kubectl get svc
     ```

### 6. **Access NGINX Application**
   - If using Minikube, retrieve the external IP:
     ```bash
     minikube service nginx-deployment
     ```
   - Access the NGINX application via the browser using the Minikube IP address.

### 7. **Troubleshooting**
   - Troubleshoot deployment issues:
     - Check Pod logs if there are issues with the NGINX application:
       ```bash
       kubectl logs <nginx-pod-name>
       ```
     - If the service is not exposed correctly, verify the service configuration:
       ```bash
       kubectl describe svc nginx-deployment
       ```

   - If the service does not show up, verify the deployment and correct any configuration issues:
     ```bash
     kubectl describe deployment nginx-deployment
     ```

   - If kubectl encounters issues with Docker contexts, reset or configure Docker context:
     ```bash
     docker context use default
     ```

### 8. **Scaling the NGINX Deployment**
   - Scale the deployment to handle more traffic:
     ```bash
     kubectl scale deployment nginx-deployment --replicas=3
     ```
   - Verify the scaled pods:
     ```bash
     kubectl get pods
     ```

### 9. **Rolling Update and Restart**
   - To perform a rolling update:
     ```bash
     kubectl rollout restart deployment nginx-deployment
     ```

   - To check the rollout status:
     ```bash
     kubectl rollout status deployment nginx-deployment
     ```

## Real-World Usage and Correlation

- **Microservices**: Kubernetes orchestrates multiple services in production environments, just like platforms such as Netflix, Uber, and Spotify.
- **NGINX as Reverse Proxy**: NGINX handles traffic distribution and load balancing in large-scale apps.
- **Scaling and High Availability**: Kubernetes automatically scales the app based on demand, ensuring high availability and performance.
- **CI/CD**: Kubernetes is integrated into DevOps pipelines for continuous delivery, similar to how large tech companies manage their deployments.
  
## Troubleshooting Tips

1. **Unable to Connect to Docker CLI Context**: Ensure that Docker is running and the context is set correctly. Use the following command to set the default Docker context:
   ```bash
   docker context use default
