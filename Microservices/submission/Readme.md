
# Kubernetes Manifests for E-Commerce Microservices

This folder contains Kubernetes manifests to deploy the E-Commerce microservices application on a Kubernetes cluster (e.g., Minikube).

## Microservices

- **User Service** (`port: 3000`)
- **Product Service** (`port: 3001`)
- **Order Service** (`port: 3002`)
- **Gateway Service** (`port: 3003`)

Each service has its own `deployment.yaml` and `service.yaml` in their respective subfolders.

## Folder Structure

```
submission/
├── deployments/
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   └── gateway-service.yaml
├── services/
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   └── gateway-service.yaml
├── ingress/              # Only if Bonus Task is attempted
│   └── ingress.yaml
├── screenshot.zip   
│   
└── README.md
```

---

## Minikube Setup

1. **Start Minikube:**
   ```sh
   minikube start
   ```

2. **(Optional) Enable Ingress add-on:**
   ```sh
   minikube addons enable ingress
   ```

---

## Deployment Steps

1. **Create a Namespace (optional):**
   ```sh
   kubectl create namespace ecom-app
   ```

2. **Deploy Microservices:**
   ```sh
   kubectl apply -f deployments/ -n ecom-app
   kubectl apply -f services/ -n ecom-app
   ```

3. **(Optional) Deploy Ingress:**
   ```sh
   kubectl apply -f ingress/ingress.yaml -n ecom-app
   ```

---

## Testing & Validation

1. **Check Running Pods:**
   ```sh
   kubectl get pods -n ecom-app
   ```

2. **Port Forward for Local Testing:**
   ```sh
   kubectl port-forward svc/user-service 3000:3000 -n ecom-app
   kubectl port-forward svc/product-service 3001:3001 -n ecom-app
   kubectl port-forward svc/order-service 3002:3002 -n ecom-app
   kubectl port-forward svc/gateway-service 3003:3003 -n ecom-app
   ```

3. **Test Service Communication:**
   - Use `curl` or Postman to hit the forwarded ports.
   - Example:
     ```sh
     curl http://localhost:3000/health
     ```

4. **Check Logs:**
   ```sh
   kubectl logs <pod-name> -n ecom-app
   ```

---

## Troubleshooting

- **Pods not starting:**  
  Check logs with `kubectl logs <pod-name> -n ecom-app`
- **Service not reachable:**  
  Ensure correct port-forwarding and service names.
- **Image pull errors:**  
  Make sure your images are pushed to Docker Hub or accessible to Minikube.
- **Ingress not working:**  
  Ensure Ingress add-on is enabled and DNS/hosts file is configured for `ecommerce.local`.

---
   ```
### Apply Ingress (if using Ingress Controller):**
   ```sh
   kubectl apply -f ingress/ingress.yaml -n ecom-app
   ```
   ---
   ### Local testing:
   
![user-service](https://github.com/user-attachments/assets/a2a0b3e5-eea7-455f-960e-c5e128cf8585)
![product-service](https://github.com/user-attachments/assets/e963a4c7-d099-4b7f-8645-b42c06e72202)
![order-service](https://github.com/user-attachments/assets/3c298b63-c098-4199-9a8f-587f3ff86c08)
![gateway-service](https://github.com/user-attachments/assets/8f591d2f-9303-4a27-956a-3e5c87c144de)

---

### Pods ,Service and Ingress :

![service](https://github.com/user-attachments/assets/cfa7621d-0333-4c57-bef5-6099c8e091a4)
![pods-status](https://github.com/user-attachments/assets/6a3576cc-70ce-40d0-8f71-df90a7ca618b)
![Ingress-details](https://github.com/user-attachments/assets/cc7f2f4e-1e47-4091-898c-1d9fe2d1f406)

---

### Logs:

<img width="1497" height="416" alt="image" src="https://github.com/user-attachments/assets/adb1ca90-20fb-44f1-9822-b1b13e7d77bd" />

---

### After applying Ingress :

<img width="967" height="508" alt="image" src="https://github.com/user-attachments/assets/d526b9f9-9e9d-45a9-803b-6cc4376ef116" />

<img width="1049" height="598" alt="image" src="https://github.com/user-attachments/assets/e00f39c3-0609-4cd2-8552-a62b82cec8de" />

<img width="377" height="158" alt="image" src="https://github.com/user-attachments/assets/c5b3b88b-08d3-42e0-a298-198107cd377d" />

<img width="933" height="366" alt="image" src="https://github.com/user-attachments/assets/0a7ef04d-8ed3-4b55-9ed0-4221b5982b69" />


## Notes

- Make sure your Docker images are available to your Kubernetes cluster (push to Docker Hub or use Minikube's Docker daemon).
- The [ingress/ingress.yaml](ingress/ingress.yaml) file sets up routing for all services under the `ecommerce.local` host.

---
