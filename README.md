

#  Capstone Project

## ( Deploying WordPress with MySQL on a Local Kubernetes Cluster )

<img width="2544" height="2128" alt="diagram-1771728150913" src="https://github.com/user-attachments/assets/474dd131-43f0-408a-9e67-1da103bd1c29" />

##  Project Overview

This project demonstrates how to deploy a **WordPress application** with a **MySQL database** using **Kubernetes on a local cluster** (kubeadm).

The project covers:

* Containerized application deployment
* Persistent storage using Kubernetes PV & PVC
* Secure secret management
* Service exposure
* Application-to-database communication inside the cluster

---

##  Architecture Overview

The solution consists of two main components:

###  MySQL Layer

* Kubernetes **Deployment**
* Kubernetes **ClusterIP Service**
* Kubernetes **Secret** for credentials
* **PersistentVolume (PV)**
* **PersistentVolumeClaim (PVC)**

###  WordPress Layer

* Kubernetes **Deployment**
* Kubernetes **Service (NodePort)**
* **PersistentVolume (PV)**
* **PersistentVolumeClaim (PVC)**
* Connects internally to MySQL service

---

##  Technologies Used

* Kubernetes (Local Cluster)
* Docker
* kubectl
* WordPress
* MySQL

---

##  Project Structure

```
.
├── mysql-secret.yaml
├── mysql-deployment.yaml
├── mysql-service.yaml
├── mysql-pv.yaml
├── mysql-pvc.yaml
├── wordpress-deployment.yaml
├── wordpress-service.yaml
├── wordpress-pv.yaml
├── wordpress-pvc.yaml
└── README.md
```

---

##  Prerequisites

Before deployment, ensure you have:

* Docker installed
* Kubernetes local cluster running:

  * Minikube OR
  * Kind OR
  * Docker Desktop Kubernetes
* kubectl configured

Check cluster:



---

##  Deployment Steps

###  Create MySQL Secret

```bash
kubectl apply -f mysql-secret.yaml
```

---

###  Deploy MySQL Resources

```bash
kubectl apply -f mysql-pv.yaml
kubectl apply -f mysql-pvc.yaml
kubectl apply -f mysql-deployment.yaml
kubectl apply -f mysql-service.yaml
```

Verify:

```bash
kubectl get pods
kubectl get svc
kubectl get pvc
```

---

###  Deploy WordPress Resources

```bash
kubectl apply -f wordpress-pv.yaml
kubectl apply -f wordpress-pvc.yaml
kubectl apply -f wordpress-deployment.yaml
kubectl apply -f wordpress-service.yaml
```

---

##  Accessing WordPress

If using **Minikube**:

```bash
minikube service wordpress-service
```

If using **NodePort**:

```bash
kubectl get svc
```

Access:

```
http://<Node-IP>:<NodePort>
```

If using Docker Desktop Kubernetes:

```
http://localhost:<NodePort>
```

---

##  Storage Details

Both MySQL and WordPress use:

* PersistentVolume (PV)
* PersistentVolumeClaim (PVC)
* Local storage (hostPath or default storage class)

This ensures:

* Data is not lost if pods restart
* MySQL database remains persistent
* WordPress files remain saved

---

##  Security

* MySQL root password stored in Kubernetes Secret
* No hardcoded credentials inside deployment files

---



##  Troubleshooting

Check logs:

```bash
kubectl logs <pod-name>
```

Describe pod:

```bash
kubectl describe pod <pod-name>
```

Check PVC binding:

```bash
kubectl get pvc
```

---

##  Learning Outcomes

Through this project, you will understand:

* Kubernetes Deployments
* Services (ClusterIP & NodePort)
* Secrets management
* Persistent Volumes & Claims
* Multi-tier application architecture
* Internal service communication in Kubernetes


