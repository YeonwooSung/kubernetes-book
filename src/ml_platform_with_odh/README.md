# Kuberentes + Open Data Hub

ODH (Open Data Hub) is an opensource project that provides most of the components that are needed for machine learning platform.
The strong point of ODH operator is that it is super simple to replace the basic components with the custom ones.

Below are the components that we are using for this platform:

- Open Data Hub: managing the lifecycle of the ML components
- JupyterHub: providing the Jupyter notebook for the users
- Apache Spark: for distributed data processing
- Seldon Core: for deploying the ML models
- Apache Airflow: for scheduling the ML pipelines (workflow engine)
- Prometheus: for monitoring the platform
- MinIO: for storing the data
- MLflow: for tracking the ML experiments
- Keycloak: for authentication and authorization (could be replaced with other identity providers)

## Prerequisites

- Kubernetes and kubectl
- Operator Lifecycle Manager (OLM)

## Running Instructions

### Set up ODH Operator

1. Register the catalog source for the Open Data Hub operator:

```bash
# Check if pods for OLM are running
kubectl get pods -n olm

# Register the catalog source
kubectl apply -f catalog-source.yaml

# After few minutes, check if the catalog source is ready
kubectl get packagemanifest -o wide -n olm | grep opendatahub
```

2. Subscribe to the Open Data Hub operator:

```bash
# Create the subscription
kubectl create -f odh-subscription.yaml

# Check if the operator is running
kubectl get pods -n operators

# Check the status of the subscription
kubectl describe -f odh-subscription.yaml
```

### Add ingress

I am currently using minikube for the development environment.
In minikube, you can add the ingress by running the following command:

```bash
minikube addons enable ingress
```

Currently, minikube and kubernetes community use `ingress-nginx` as the default ingress controller.
So, by using the above command, you can add the ingress controller to your minikube.

```bash
# get the pods for ingress-nginx
kubectl get pods -n ingress-nginx
```

### Keycloak for Authentication

Keycloak is an open-source identity and access management for modern applications and services.
It supports OpenID Connect, OAuth 2.0, and SAML.

```bash
# Create the namespace for keycloak
kubectl create namespace keycloak

# Create manifests for keycloak
kubectl create -f keycloak.yaml --namespace keycloak

# Check the status of the keycloak pods
kubectl get pods -n keycloak
```

I was not able to run this on my M1 Macbook Pro, since the image is not available for the ARM architecture.
