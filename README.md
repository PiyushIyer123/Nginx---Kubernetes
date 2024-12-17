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

   # Real-Time Usage & Correlation with Real-World Scenarios

## Microservices Architecture

Many modern applications are built using microservices, where different parts of the app (e.g., authentication, user profile, payment gateway) are developed, deployed, and managed independently. Kubernetes allows each microservice to run in isolated containers, orchestrated across a cluster of machines.

**Example**: Large-scale platforms like Netflix, Uber, or Spotify use Kubernetes to run their microservices in containers, ensuring that the different services can scale independently based on demand and recover automatically if any service fails.

## NGINX as a Reverse Proxy & Load Balancer

In your lab, you deployed NGINX, which is commonly used as a reverse proxy and load balancer in production environments. When an application is exposed to the internet, NGINX acts as the entry point to route traffic to the correct backend service.

**Example**: Websites like Twitter, Instagram, or GitHub often use NGINX to route traffic between frontend services and backend APIs. NGINX helps distribute the incoming traffic evenly across multiple instances of a service to ensure that no single instance is overwhelmed, enhancing performance and reliability.

## Scaling Applications

Kubernetes enables auto-scaling of applications. For instance, if your web application (like the NGINX deployment in your lab) experiences a spike in traffic, Kubernetes can scale the number of pod replicas to handle the additional load.

**Example**: Amazon, Airbnb, and Snapchat use Kubernetes to scale their applications dynamically based on the traffic patterns. If there’s a sudden surge in users during peak hours, Kubernetes automatically adds more instances of services (e.g., web servers, database connections) to handle the load without manual intervention.

## Continuous Deployment and DevOps

Kubernetes is an integral part of the DevOps pipeline, enabling continuous integration and continuous deployment (CI/CD). Developers push their code to repositories (e.g., GitHub), and CI/CD tools automatically build the containerized application and deploy it to Kubernetes clusters. This automates testing, building, and deploying updates without downtime.

**Example**: Apps like GitHub, Slack, and Facebook continuously deploy new features, bug fixes, and updates. Kubernetes ensures that these changes are rolled out without affecting the user experience.

## Infrastructure as Code (IaC)

In your lab, you used Kubernetes commands to manage deployments and services. In the real world, this can be automated using Infrastructure as Code tools like Terraform, Helm, or Kustomize. These tools allow infrastructure to be defined and managed in configuration files, making the deployment process repeatable, scalable, and auditable.

**Example**: Google Cloud and AWS users can define their Kubernetes infrastructure using IaC tools, ensuring consistency across multiple environments (dev, staging, production).

## Apps You Use Daily that Work on These Technologies

Here are a few popular apps and services that use Kubernetes in their backend, often relying on NGINX or similar technologies for traffic routing, scaling, and availability:

- **Spotify**: 
  Spotify uses Kubernetes to manage its microservices, which handle everything from streaming music to managing user playlists and recommendations. The NGINX or similar reverse proxy setup ensures smooth traffic routing and load balancing.

- **Uber**: 
  Uber relies on Kubernetes to orchestrate a fleet of microservices, including rider matching, payment systems, and push notifications. This enables Uber to handle millions of users concurrently and scale its services up and down based on demand.

- **Slack**: 
  Slack leverages Kubernetes to manage its messaging platform's backend services, ensuring that messages, files, and notifications are delivered in real-time, and that the infrastructure scales to meet the needs of millions of users.

- **GitHub**: 
  GitHub, the popular code-hosting platform, uses Kubernetes for its backend services to ensure that code is always available, commits are processed efficiently, and the platform can handle millions of concurrent users across different geographies.

- **Airbnb**: 
  Airbnb uses Kubernetes for deploying and managing services that power its website and mobile app, including user accounts, bookings, payment systems, and notifications. Kubernetes' auto-scaling ensures that Airbnb can handle peak demand (such as during holidays or events) without downtime.

## Takeaways for Real-World Applications

- **High Availability & Reliability**: Just like in the lab, Kubernetes ensures that services like NGINX (or any other service) are highly available, resilient to failures, and can scale dynamically.
  
- **Traffic Management**: The use of NGINX in your lab as a reverse proxy/load balancer mirrors how large-scale apps manage traffic, ensuring no single server is overwhelmed by requests.

- **Efficient Scaling**: Kubernetes allows apps to handle massive traffic spikes without downtime, just like how companies like Uber, Netflix, and Airbnb can serve millions of users simultaneously.

By using Kubernetes and technologies like NGINX, developers can ensure their apps are performant, scalable, and highly available — qualities that are crucial for any app or service used in the real world today.

