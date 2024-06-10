# Kubernetes Deployment Instructions
This guide will help you deploy your project using Kubernetes with Minikube. Follow the steps below to set up and access your application.

## Prerequisites
- Ensure you have Minikube installed and running.
- Ensure `kubectl` is installed and configured to communicate with your Minikube cluster.

## Deployment Steps
1. **Run minikube:**
   ```sh
   minikube start --driver=docker --mount --mount-string="/tmp/plant-it-data:/mnt/data"
   ```

2. **Deploy the DB Secrets:**
   ```sh
   kubectl apply -f db-secret.yml
   ```

3. **Deploy the DB ConfigMaps:**
   ```sh
   kubectl apply -f db-config.yml
   ```

4. **Deploy the Database:**
   ```sh
   kubectl apply -f db.yml
   ```

5. **Deploy the Cache:**
   ```sh
   kubectl apply -f cache.yml
   ```

6. **Deploy the Server:**
   ```sh
   kubectl apply -f server.yml
   ```

## Access the Application
Once the deployment is complete, you can access the application and its Swagger UI at the following URLs:

- **Application:** `http://<minikube_ip>:3000`
- **Swagger UI:** `http://<minikube_ip>:8080/api/swagger-ui/index.html`

Replace `<minikube_ip>` with the IP address returned by the following command:

```sh
minikube ip
```

### ⚠ Known Issue - Minikube IP not Accessible
If you encounter issues accessing the NodePort service using `MinikubeIP:NodePort`, execute the following command to expose the service and obtain a direct URL:

```sh
minikube service server-service
```

Then, open the printed links in your browser to access the application and Swagger UI.
