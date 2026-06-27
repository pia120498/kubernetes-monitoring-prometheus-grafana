# Kubernetes Monitoring & Observability Platform

A production-inspired monitoring platform built using **Flask**, **Docker**, **Kubernetes**, **Prometheus**, **Grafana**, and **Node Exporter**. This project demonstrates end-to-end deployment, application monitoring, infrastructure monitoring, alerting, and visualization in a Kubernetes environment.

---

## Project Overview

This project deploys a Python Flask application on Kubernetes and implements a complete monitoring stack to observe both application and infrastructure metrics.

The monitoring solution includes:

- Application metrics exposed using Prometheus Python Client
- Prometheus for metrics collection and alerting
- Grafana dashboards for visualization
- Node Exporter for infrastructure metrics
- Persistent storage for Prometheus and Grafana
- Kubernetes Deployments, Services, ConfigMaps and Persistent Volume Claims

---

## Architecture

<img width="725" height="681" alt="Screenshot 2026-06-28 010501" src="https://github.com/user-attachments/assets/a2018a79-3b92-48ea-9826-bd0c88aff4fa" />


---

## Tech Stack

| Category | Technologies |
|----------|--------------|
| Language | Python |
| Framework | Flask |
| Containerization | Docker |
| Container Orchestration | Kubernetes (Minikube) |
| Monitoring | Prometheus |
| Visualization | Grafana |
| Infrastructure Metrics | Node Exporter |
| Alerting | Prometheus Alert Rules |
| Version Control | Git & GitHub |

---


# Dashboard Preview

### Kubernetes Observability Dashboard

<img width="1918" height="955" alt="Screenshot 2026-06-28 012443" src="https://github.com/user-attachments/assets/f127ae54-6bfe-4d26-b863-76120cbf211e" />

---

# Alert Verification

### Monitoring Application Down

Pending

<img width="1918" height="591" alt="App-down-alert-pending" src="https://github.com/user-attachments/assets/9eac8029-ae93-4c4d-b6ab-abbee25555eb" />

Firing

<img width="1917" height="618" alt="App-down-alert-firing" src="https://github.com/user-attachments/assets/6c7a029c-c2aa-4e9a-ad17-4907ee8fddf2" />


Resolved

<img width="1905" height="633" alt="App-down-alert-resolved" src="https://github.com/user-attachments/assets/55b5389e-263d-477f-a502-d37e68933365" />

---

# Prometheus Targets

Successfully scraping:

- Monitoring Application
- Node Exporter

<img width="1919" height="757" alt="image" src="https://github.com/user-attachments/assets/0cd90714-ca92-4bbe-beda-f004f6cfefb4" />


---


# Project Features

### Application Deployment

- Flask web application
- Dockerized application
- Kubernetes Deployment
- Kubernetes Service (NodePort)

---

### Monitoring

- Prometheus metrics endpoint (`/metrics`)
- Custom HTTP Request Counter
- Application CPU metrics
- Process metrics
- Prometheus scraping configuration

---

### Infrastructure Monitoring

Using Node Exporter:

- CPU Usage
- Memory Usage
- Node Uptime
- Host Metrics

---

### Grafana Dashboard

Custom dashboard includes:

- Application Status
- Total HTTP Requests
- Application CPU Time
- Node CPU Usage
- Node Memory Usage
- Node Uptime

---

### Alerting

Configured Prometheus alert rules for:

- Monitoring Application Down
- High CPU Usage
- High Memory Usage

Alerts were successfully tested through:

- Pending State
- Firing State
- Resolved State

---

### Persistent Storage

Configured Persistent Volume Claims for:

- Prometheus
- Grafana

Verified that Grafana dashboards persist after pod recreation.

---


# Repository Structure

```text
k8s-monitoring-project/
│
├── app/
│   ├── app.py
│   ├── Dockerfile
│   ├── requirements.txt
│   └── .dockerignore
│
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
│
├── monitoring/
│   ├── grafana/
│   │   ├── dashboard.json
│   │   ├── grafana-deployment.yaml
│   │   ├── grafana-pvc.yaml
│   │   └── grafana-service.yaml
│   │
│   ├── node-exporter/
│   │   ├── node-exporter-deployment.yaml
│   │   └── node-exporter-service.yaml
│   │
│   └── prometheus/
│       ├── alert-rules.yaml
│       ├── prometheus-config.yaml
│       ├── prometheus-deployment.yaml
│       ├── prometheus-pvc.yaml
│       └── prometheus-service.yaml
│
├── screenshots/
│   ├── dashboard.png
│   ├── prometheus-targets.png
│   ├── alert-pending.png
│   ├── alert-firing.png
│   ├── alert-resolved.png
│   ├── kubectl-pods.png
│   ├── kubectl-pvc.png
│   └── architecture-diagram.png
│
├── .gitignore
└── README.md```


# Getting Started

## Clone Repository

```bash
git clone https://github.com/<your-username>/k8s-monitoring-project.git

cd k8s-monitoring-project
```

---

## Build Docker Image

```bash
docker build -t monitoring-app .
```

---

## Deploy Application

```bash
kubectl apply -f k8s/
```

---

## Deploy Prometheus

```bash
kubectl apply -f monitoring/prometheus/
```

---

## Deploy Node Exporter

```bash
kubectl apply -f monitoring/node-exporter/
```

---

## Deploy Grafana

```bash
kubectl apply -f monitoring/grafana/
```

---

## Verify Pods

```bash
kubectl get pods
```

---

## Verify Services

```bash
kubectl get svc
```

---

# Useful PromQL Queries

Application Status

```promql
up
```

HTTP Requests

```promql
http_requests_total
```

Application CPU Time

```promql
process_cpu_seconds_total
```

CPU Usage

```promql
100 - (avg by(instance)(rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
```

Memory Usage

```promql
100 * (1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes))
```

Node Uptime

```promql
node_time_seconds - node_boot_time_seconds
```

---



⭐ If you found this project useful, consider giving it a star.
