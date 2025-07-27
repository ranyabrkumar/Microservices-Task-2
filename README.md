# E-Commerce Microservices Kubernetes Deployment

This repository contains Kubernetes manifests and documentation for deploying a Node.js-based e-commerce microservices application on Minikube.

## Table of Contents

- [Overview](#overview)
- [Folder Structure](#folder-structure)
- [Minikube Setup](#minikube-setup)
- [Deployment Steps](#deployment-steps)
- [Testing & Validation](#testing--validation)
- [Troubleshooting](#troubleshooting)
- [Screenshots](#screenshots)
- [Bonus: Ingress Setup](#bonus-ingress-setup)

---

## Overview

The application consists of four microservices:

- **User Service** (`port: 3000`)
- **Product Service** (`port: 3001`)
- **Order Service** (`port: 3002`)
- **Gateway Service** (`port: 3003`)

Each service has its own Kubernetes deployment and service manifest. Optionally, an Ingress resource is provided for unified routing.

---

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
├── screenshots/
│   ├── pods.png
│   ├── logs.png
│   └── service-test.png
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

## Screenshots

- `screenshots/pods.png` – Output of `kubectl get pods`
- `screenshots/logs.png` – Example logs showing service communication
- `screenshots/service-test.png` – Example of successful port-forwarded request

---

## Bonus: Ingress Setup

If you attempt the bonus:

- Ingress routes:
  - `/api/users` → User Service
  - `/api/products` → Product Service
  - `/api/orders` → Order Service
  - `/` → Gateway Service

- Access via:  
  `http://ecommerce.local/api/users`, etc.

---
