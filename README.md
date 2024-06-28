# WordPress with Kubernetes and Docker

This project deploys a WordPress application using Kubernetes and Docker, utilizing Helm charts for easier management and configuration.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Project Structure](#project-structure)
3. [Setup Instructions](#setup-instructions)
    - [Step 1: Clone the Repository](#step-1-clone-the-repository)
    - [Step 2: Build Docker Images](#step-2-build-docker-images)
    - [Step 3: Push Docker Images to a Repository](#step-3-push-docker-images-to-a-repository)
    - [Step 4: Deploy WordPress with Helm](#step-4-deploy-wordpress-with-helm)
    - [Step 5: Access the WordPress Application](#step-5-access-the-wordpress-application)
4. [Configuration](#configuration)
5. [Cleanup](#cleanup)
6. [Contributing](#contributing)
7. [License](#license)

## Prerequisites

Before you begin, ensure you have the following software installed:

- [Docker](https://docs.docker.com/get-docker/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Helm](https://helm.sh/docs/intro/install/)

## Project Structure

The project includes the following key files and directories:


├── MySQL

│ └── Dockerfile

├── nginx

│ └── Dockerfile

│ └── nginx.config

├── Wordpress

│ └── Dockerfile

├── wordpress-chart

│ ├── Chart.yaml

│ ├── values.yaml

│ └── templates

│ ├── deployment.yaml

│ ├── service.yaml

│ └── ingress.yaml

├── pvs.yaml

├── pvcs.yaml

└── README.md

## Setup Instructions

### Step 1: Clone the Repository

Clone the repository to your local machine:

```bash
git clone https://github.com/username/wordpress-project.git
cd wordpress-project
```

### Step 2: Set Up PersistentVolumes and PersistentVolumeClaims
Create PVs and PVCs with ReadWriteMany access mode.

```
kubectl apply -f pvs.yaml
kubectl apply -f pvcs.yaml
```

## Step 3: Build Docker Images
Build the required Docker images for WordPress, MySQL, and Nginx.

```
# Build MySQL image
cd mysql
docker build -t myrepo/mysql:latest .

# Build Nginx image
cd ../nginx
docker build -t myrepo/nginx:latest .

# Build WordPress image
cd ../wordpress
docker build -t myrepo/wordpress:latest .
```
## Step 4: Push Docker Images to a Repository
Push the Docker images to your repository

```
# Login to your Docker repository
docker login

# Push MySQL image
docker push myrepo/mysql:latest

# Push Nginx image
docker push myrepo/nginx:latest

# Push WordPress image
docker push myrepo/wordpress:latest
```
## Step 5: Deploy WordPress with Helm
Deploy the WordPress application using Helm:

```
helm install my-release ./wordpress-chart
```
This command will install the WordPress release using the Helm chart located in the wordpress-chart directory.

## Step 6: Access the WordPress Application
Get the URL to access the WordPress application:

```
minikube service my-release-wordpress-chart --url
```
Open the provided URL in your web browser to access your WordPress site.

## Configuration

## values.yaml
The values.yaml file contains configuration values for the Helm chart. You can customize the deployment by modifying this file. Key sections include:

replicaCount: Number of replicas for the deployment.

image: Docker image information.

service: Service type and port configuration.

ingress: Ingress configuration for external access.

resources: Resource requests and limits for the containers.

## deployment.yaml
The deployment for the WordPress application, including container specifications, probes, and volume mounts.

## service.yaml
The services for the WordPress, MySQL, and nginx applications. 

## pvc.yaml
PersistentVolumeClaims for WordPress and MySQL data storage.

## Cleanup
To remove the WordPress deployment and free up resources, run:

```
helm delete my-release
```

To stop Minikube, run:

```
minikube stop
```

## Contributing
Contributions are welcome! Please fork the repository and create a pull request with your changes.

## License
This project is licensed under the MIT License.







