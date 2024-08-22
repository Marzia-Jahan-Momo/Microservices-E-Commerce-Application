# Microservices E-Commerce Application

This repository contains the code for a microservices-based e-commerce application. Each microservice is responsible for a specific functionality within the application, and all services are containerized with Docker. Kubernetes manifests for deploying these services are also included.

## Repository Structure

- **src/**: Contains the source code for all microservices. Each microservice has its own directory with a corresponding `Dockerfile` for building the container image.
  
- **Kubernetes Manifest/**: Contains Kubernetes manifests for deploying the microservices. The manifests are organized as follows:
  - **Individual Manifests/**: Kubernetes manifests for each microservice individually.
  - **All in one k8s manifest.yaml**: A single YAML file to deploy all microservices together.

## Microservices Overview

### Frontend (`Go`)
- **Description**: Exposes an HTTP server to serve the website. Does not require signup/login and generates session IDs for all users automatically.
- **Location**: `src/frontend/`
- **Docker Image**: `docker pull jahanmomo19/microservice:frontend`

### Cart Service (`C#`)
- **Description**: Stores the items in the user's shopping cart in Redis and retrieves it.
- **Location**: `src/cartservice/`
- **Docker Image**: `docker pull jahanmomo19/microservice:cartservice`

### Product Catalog Service (`Go`)
- **Description**: Provides the list of products from a JSON file and allows searching products and getting individual products.
- **Location**: `src/productcatalogservice/`
- **Docker Image**: `docker pull jahanmomo19/microservice:productcatalogservice`

### Currency Service (`Node.js`)
- **Description**: Converts one money amount to another currency using real-time exchange rates from the European Central Bank. This is the highest QPS (queries per second) service.
- **Location**: `src/currencyservice/`
- **Docker Image**: `docker pull jahanmomo19/microservice:currencyservice`

### Payment Service (`Node.js`)
- **Description**: Charges the given credit card information (mock) with the specified amount and returns a transaction ID.
- **Location**: `src/paymentservice/`
- **Docker Image**: `docker pull jahanmomo19/microservice:paymentservice`

### Shipping Service (`Go`)
- **Description**: Provides shipping cost estimates based on the shopping cart and ships items to the given address (mock).
- **Location**: `src/shippingservice/`
- **Docker Image**: `docker pull jahanmomo19/microservice:shippingservice`

### Email Service (`Python`)
- **Description**: Sends users an order confirmation email (mock).
- **Location**: `src/emailservice/`
- **Docker Image**: `docker pull jahanmomo19/microservice:emailservice`

### Checkout Service (`Go`)
- **Description**: Retrieves the user cart, prepares the order, and orchestrates the payment, shipping, and email notification.
- **Location**: `src/checkoutservice/`
- **Docker Image**: `docker pull jahanmomo19/microservice:checkoutservice`

### Recommendation Service (`Python`)
- **Description**: Recommends other products based on the contents of the cart.
- **Location**: `src/recommendationservice/`
- **Docker Image**: `docker pull jahanmomo19/microservice:recommendationservice`

### Ad Service (`Java`)
- **Description**: Provides text ads based on given context words.
- **Location**: `src/adservice/`
- **Docker Image**: `docker pull jahanmomo19/microservice:adservice`

### Load Generator (`Python/Locust`)
- **Description**: Continuously sends requests that imitate realistic user shopping flows to the frontend for performance testing.
- **Location**: `src/loadgenerator/`
- **Docker Image**: `docker pull jahanmomo19/microservice:loadgenerator`

## Using Docker

Each microservice's Docker image is available on Docker Hub. You can pull any of the microservices using the following command:

```bash
docker pull jahanmomo19/microservice:<microservice-name>
```

Replace `<microservice-name>` with the specific microservice, such as `frontend`, `cartservice`, `productcatalogservice`, etc.

For example:

```bash
docker pull jahanmomo19/microservice:productcatalogservice
docker pull jahanmomo19/microservice:adservice
```

## Building and Running Locally

If you prefer to build and run the services locally, navigate to the specific service directory and use the following commands:

```bash
cd src/<service_directory>
docker build -t jahanmomo19/microservice:<service_name> .
docker run -d -p <port>:<port> jahanmomo19/microservice:<service_name>
```

Replace `<service_name>` and `<port>` with the appropriate values.

## Kubernetes Deployment

Kubernetes manifests are provided to deploy these services either individually or all at once.

1. **Individual Deployment**:
   - Navigate to the ```Kubernetes Manifest/Individual Manifests/``` directory and apply the desired manifest files:
   ```bash
   kubectl apply -f <service-manifest.yaml>
   ```

2. **All-in-One Deployment**:
   - Use the `All in one k8s manifest.yaml` file to deploy all services at once:
   ```bash
   kubectl apply -f Kubernetes Manifest/All in one k8s manifest.yaml
   ```


---

©️ by Google

---
