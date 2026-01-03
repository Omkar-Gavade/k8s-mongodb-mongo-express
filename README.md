# k8s-mongodb-mongo-express

# Kubernetes MongoDB & Mongo Express Deployment

This project demonstrates deploying a real-world, multi-component application on Kubernetes using **MongoDB** and **Mongo Express**, following Kubernetes best practices such as **service-based communication**, **ConfigMaps**, and **Secrets**.

The setup is designed and tested on **Minikube** for local development and learning.

---

## Architecture Overview

The application consists of two main Pods:

- **MongoDB Pod**
  - Runs the MongoDB database
  - Exposed internally using a Kubernetes Service
  - Not accessible from outside the cluster

- **Mongo Express Pod**
  - Web-based UI for managing MongoDB
  - Exposed externally using a Kubernetes Service
  - Connects to MongoDB via internal service DNS

### Traffic Flow
1. User sends request from browser
2. Request reaches Mongo Express via external Service
3. Mongo Express connects to MongoDB using internal Service
4. MongoDB returns data
5. Response is displayed in the browser

---

## Kubernetes Components Used

### 1. Deployments
- MongoDB Deployment
- Mongo Express Deployment  
Used to manage Pods, replicas, and container lifecycle.

### 2. Services
- **Internal Service** for MongoDB (cluster-only access)
- **External Service** for Mongo Express (NodePort access)

Services provide stable networking and load balancing between Pods.

### 3. ConfigMap
Used to store **non-sensitive configuration data**, such as:
- MongoDB service name / database connection info

This keeps configuration separate from application code.

### 4. Secret
Used to store **sensitive data**, such as:
- MongoDB username
- MongoDB password

Secrets are injected into containers as environment variables to avoid hardcoding credentials.

---

## Project Structure
kubernetes/
├── mongodb-deployment.yaml
├── mongodb-service.yaml
├── mongodb-configmap.yaml
├── mongodb-secret.yaml
├── mongo-express-deployment.yaml
├── mongo-express-service.yaml
├── README.md

---

## Prerequisites

- Docker
- Minikube
- kubectl

---

## How to Run the Project

### 1. Start Minikube
```bash
minikube start

Key Learnings
	•	Deploying multi-service applications on Kubernetes
	•	Internal vs external Services
	•	Service-to-service communication using DNS
	•	Using ConfigMaps for configuration
	•	Using Secrets for secure credential management
	•	Debugging Pods, Services, and Endpoints
	•	Understanding real Kubernetes traffic flow