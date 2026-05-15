# KUBERNETES NOTES

# What is Kubernetes?

Kubernetes (K8s) is a container orchestration platform.

Docker can run containers.
But managing hundreds of containers manually becomes difficult.

Kubernetes helps automate:

- deployment
- scaling
- monitoring
- networking
- self healing

Main idea:
Manage containers at large scale.

---

# Why Kubernetes is Needed

Suppose:
Application has:

- frontend
- backend
- database
- redis
- authentication service

Now imagine:
1000 users accessing application.

Problems:

- Containers may crash
- Traffic increases
- Manual scaling difficult
- Downtime issues

Kubernetes solves these.

---

# Important Understanding

Docker = container runtime

Kubernetes = container manager

Both usually work together.

---

# Kubernetes Architecture

Cluster contains:

1. Control Plane
2. Worker Nodes

---

# Control Plane Components

## API Server

Main entry point.

All kubectl commands go through API server.

## Scheduler

Decides where pod should run.

## Controller Manager

Checks desired state vs actual state.

## etcd

Database storing cluster information.

---

# Worker Node Components

## kubelet

Communicates with control plane.

## kube-proxy

Handles networking.

## Container Runtime

Runs containers.

Example:
containerd
Docker

---

# Important Terms

## Cluster

Collection of nodes.

## Node

Machine inside cluster.

## Pod

Smallest deployable unit.

Usually contains:
1 container + networking/storage

Important:
Kubernetes manages pods, not containers directly.

---

# Installing Minikube

Minikube is easiest for beginners.

Start cluster:

```bash
minikube start
```

Check status:

```bash
minikube status
```

---

# kubectl

kubectl is Kubernetes CLI tool.

Check version:

```bash
kubectl version
```

Cluster info:

```bash
kubectl cluster-info
```

---

# First Practical I Performed

Checked nodes:

```bash
kubectl get nodes
```

Output showed:

- node name
- status
- role
- age

---

# Creating First Deployment

```bash
kubectl create deployment nginx --image=nginx
```

What happened internally:

1. Deployment created
2. ReplicaSet created
3. Pod created
4. Container started

---

# Viewing Pods

```bash
kubectl get pods
```

Observed:
Pod names are auto generated.

Detailed output:

```bash
kubectl get pods -o wide
```

---

# Understanding Pod Lifecycle

Pod states:

- Pending
- Running
- Succeeded
- Failed
- CrashLoopBackOff

---

# Describing Pods

```bash
kubectl describe pod <pod_name>
```

Useful for debugging.

Shows:

- events
- image
- node
- IP
- errors

---

# Viewing Logs

```bash
kubectl logs <pod_name>
```

Follow logs:

```bash
kubectl logs -f <pod_name>
```

---

# Executing Commands Inside Pod

```bash
kubectl exec -it <pod_name> -- bash
```

Commands I tested:

```bash
ls
pwd
nginx -v
```

---

# YAML Files

Kubernetes mainly works using YAML manifests.

---

# My First Pod YAML

pod.yaml:

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  containers:
    - name: nginx
      image: nginx
```

Apply:

```bash
kubectl apply -f pod.yaml
```

Check:

```bash
kubectl get pods
```

---

# Understanding YAML Fields

## apiVersion

Version of Kubernetes API.

## kind

Type of object.

Examples:
Pod
Deployment
Service

## metadata

Information about object.

## spec

Actual configuration.

---

# Deployments

Deployment manages pods.

Features:

- scaling
- updates
- rollback
- self healing

deployment.yaml:

```yaml
apiVersion: apps/v1

kind: Deployment

metadata:
  name: nginx-deployment

spec:
  replicas: 2

  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx

    spec:
      containers:
        - name: nginx
          image: nginx
```

Apply:

```bash
kubectl apply -f deployment.yaml
```

---

# Scaling Deployment

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

Observed:
New pods automatically created.

---

# Deleting Pods

Deleted one pod manually:

```bash
kubectl delete pod <pod_name>
```

Interesting observation:
Kubernetes recreated pod automatically.

Reason:
Deployment wanted desired replicas.

This is called self-healing.

---

# Services

Pods have dynamic IPs.

Need stable access mechanism.

Solution:
Services.

---

# Types of Services

## ClusterIP

Internal communication.

## NodePort

Exposes outside cluster.

## LoadBalancer

Used in cloud environments.

---

# NodePort Practical

service.yaml:

```yaml
apiVersion: v1
kind: Service

metadata:
  name: nginx-service

spec:
  type: NodePort

  selector:
    app: nginx

  ports:
    - port: 80
      targetPort: 80
      nodePort: 30007
```

Apply:

```bash
kubectl apply -f service.yaml
```

Check:

```bash
kubectl get services
```

---

# ReplicaSet

Ensures desired number of pods always running.

Usually managed by deployment.

---

# Namespaces

Used for logical separation.

Default namespaces:

- default
- kube-system
- kube-public

View:

```bash
kubectl get namespaces
```

---

# ConfigMap

Stores non-sensitive configuration.

Example:
database URL
environment variables

---

# Secret

Stores sensitive data.

Example:

- passwords
- tokens
- API keys

---

# Rolling Updates

Update image:

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:latest
```

Observed:
Pods updated gradually without downtime.

---

# Rollback

Undo deployment:

```bash
kubectl rollout undo deployment/nginx-deployment
```

---

# Checking Events

```bash
kubectl get events
```

Useful while troubleshooting.

---

# Resource Monitoring

```bash
kubectl top pods
```

```bash
kubectl top nodes
```

---

# Common Errors I Faced

1. ImagePullBackOff
   Reason:
   Wrong image name.

2. CrashLoopBackOff
   Reason:
   Application crashing repeatedly.

3. YAML indentation issue
   Most common beginner mistake.

---

# Kubernetes Networking Understanding

Each pod gets:

- unique IP
- internal communication ability

Pods can communicate with each other.

---

# Ingress

Used for routing external traffic.

Example:
domain based routing.

---

# Difference Between Docker and Kubernetes

Docker:

- Creates containers

Kubernetes:

- Manages containers at scale

Docker is not replacement for Kubernetes.
Kubernetes is not replacement for Docker.

---

# Summary

Things I understood:

- Kubernetes manages containerized applications
- Pod is smallest unit
- Deployment manages pods
- Services expose applications
- Kubernetes automatically heals failed pods

Things I should practice more:

- YAML writing
- Helm
- Ingress
- Monitoring
- Debugging

---

# Commands Cheat Sheet

```bash
kubectl get nodes
kubectl get pods
kubectl get services
kubectl describe pod <name>
kubectl logs <pod>
kubectl exec -it <pod> -- bash
kubectl apply -f file.yaml
kubectl delete pod <name>
kubectl scale deployment nginx --replicas=3
kubectl rollout undo deployment/nginx
kubectl get namespaces
```
