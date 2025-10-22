# Microservices Helm Charts Repository

This repository contains Helm charts for the Shopy-shopy microservices application.

## Repository Structure

```
microservice-helm-charts/
├── helm-charts/                 # Source Helm charts
│   ├── adservice/
│   │   ├── Chart.yaml
│   │   ├── values.yaml
│   │   └── templates/
│   ├── cartservice/
│   ├── checkoutservice/
│   ├── currencyservice/
│   ├── emailservice/
│   ├── frontend/
│   ├── loadgenerator/
│   ├── paymentservice/
│   ├── productcatalogservice/
│   ├── recommendationservice/
│   └── shippingservice/
├── charts/                     # Packaged Helm charts (.tgz files)
│   ├── adservice-0.1.0.tgz
│   ├── cartservice-0.1.0.tgz
│   └── ... other packaged charts
└── index.yaml                  # Helm repository index
```

## Services

This repository contains Helm charts for the following microservices:

- **adservice**: Advertisement service
- **cartservice**: Shopping cart service (includes Redis)
- **checkoutservice**: Checkout processing service
- **currencyservice**: Currency conversion service
- **emailservice**: Email notification service
- **frontend**: Web frontend service
- **loadgenerator**: Load testing service
- **paymentservice**: Payment processing service
- **productcatalogservice**: Product catalog service
- **recommendationservice**: Product recommendation service
- **shippingservice**: Shipping calculation service

## Usage

### Add this repository to Helm

```bash
helm repo add microservices https://raw.githubusercontent.com/Amaldeep98/microservice-helm-charts/main/
helm repo update
```

### Install a service

```bash
helm install frontend microservices/frontend
helm install cartservice microservices/cartservice
```

### Install all services

```bash
helm install adservice microservices/adservice
helm install cartservice microservices/cartservice
helm install checkoutservice microservices/checkoutservice
helm install currencyservice microservices/currencyservice
helm install emailservice microservices/emailservice
helm install frontend microservices/frontend
helm install loadgenerator microservices/loadgenerator
helm install paymentservice microservices/paymentservice
helm install productcatalogservice microservices/productcatalogservice
helm install recommendationservice microservices/recommendationservice
helm install shippingservice microservices/shippingservice
```

## Configuration

Each service has its own `values.yaml` file that can be customized. Key configuration options include:

- **Image repository**: ECR repository URLs
- **Image tags**: Version tags for Docker images
- **Resource limits**: CPU and memory limits
- **Replica count**: Number of pod replicas
- **Service configuration**: Ports and service types

## Prerequisites

- Kubernetes cluster (EKS, GKE, AKS, or local)
- Helm 3.x
- Docker images available in ECR repository
- ECR secret configured in the cluster

## ECR Configuration

All services are configured to use ECR images. Make sure to:

1. Create ECR repositories for each service
2. Build and push Docker images to ECR
3. Create ECR secret in the cluster:

```bash
kubectl create secret docker-registry ecr-secret \
  --docker-server=183611507646.dkr.ecr.us-east-1.amazonaws.com \
  --docker-username=AWS \
  --docker-password=$(aws ecr get-login-password --region us-east-1)
```

## Development

To modify charts:

1. Edit files in `helm-charts/<service>/`
2. Package the chart: `helm package helm-charts/<service>/`
3. Update the repository index: `helm repo index .`
4. Commit and push changes

## License

This project is licensed under the Apache License 2.0.
