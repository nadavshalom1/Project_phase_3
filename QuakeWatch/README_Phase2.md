QuakeWatch - Phase 2: Kubernetes Orchestration
Project Overview
This phase focuses on orchestrating the QuakeWatch Flask application using Kubernetes. The goal is to deploy a scalable, highly available application with automated health checks and periodic tasks.
Prerequisites
• Docker Desktop with Kubernetes enabled (Cluster Setup).
• kubectl CLI tool configured to communicate with the cluster.
Architecture & Resources
The project uses the following Kubernetes manifests to manage the application lifecycle:
1. Deployment (deployment.yaml):
    ◦ Manages the Pods running the QuakeWatch container.
    ◦ Includes Liveness and Readiness Probes to ensure the application is running and ready to serve traffic before receiving requests.
2. Service (service.yaml):
    ◦ Exposes the application externally so it can be accessed via a web browser.
3. Configuration & Secrets (config-secret.yaml):
    ◦ Stores sensitive data and configuration variables required by the application.
4. Horizontal Pod Autoscaler (hpa.yaml):
    ◦ Automatically scales the number of pods based on CPU utilization to handle load.
5. CronJob (cronjob.yaml):
    ◦ Runs a periodic task that attempts to connect to the application from within the cluster to verify the service uptime.
How to Deploy
1. Build the Image (if not pulling from Docker Hub)
Ensure the Docker image is available locally or pull it from the registry:
docker build -t <your-dockerhub-username>/quakewatch:latest .
2. Apply Configurations and Secrets
First, create the configuration maps and secrets:
kubectl apply -f config-secret.yaml
3. Deploy the Application
Deploy the main application logic:
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
4. Setup Autoscaling and CronJobs
Enable autoscaling and background tasks:
kubectl apply -f hpa.yaml
kubectl apply -f cronjob.yaml
Verification
• Check Status: Run kubectl get all to see running pods, services, and jobs.
• Access App: Open a browser at http://localhost:<node-port> (or the LoadBalancer IP).
• Verify HPA: Run kubectl get hpa to see scaling metrics.

