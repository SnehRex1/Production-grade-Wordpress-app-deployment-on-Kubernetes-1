﻿# Production-grade-Wordpress-app-deployment-on-Kubernetes-1
WordPress Deployment on Kubernetes using Helm
This project demonstrates how to deploy a production-grade WordPress application on Kubernetes using Helm. It includes configurations for WordPress, MySQL, and Nginx deployed with persistent volumes and a custom Nginx setup with Lua scripting.

Table of Contents
Overview
Prerequisites
Setup
1. Clone the Repository
2. Build Docker Images
3. Deploy with Helm
Usage
Accessing WordPress
Cleaning Up
Contributing
License
Overview
This project sets up WordPress on Kubernetes using Helm charts. It includes:

Persistent Volumes: Configured for WordPress and MySQL to ensure data persistence.
Custom Docker Images: Built for WordPress, MySQL, and Nginx with specific configurations.
Custom Nginx Setup: Includes Lua scripting for advanced Nginx configurations.
Prerequisites
Before you begin, ensure you have the following installed:

Docker: Version 18.09 or higher
Minikube: Version 1.22.0 or higher
Helm: Version 3.x
kubectl: Version matching your Kubernetes cluster
Setup
Follow these steps to set up the WordPress deployment:

1. Clone the Repository
bash
Copy code
git clone <repository-url>
cd wordpress-project
2. Build Docker Images
Build the required Docker images for WordPress, MySQL, and Nginx.

bash
Copy code
cd mysql
docker build -t myrepo/mysql:latest .

cd ../nginx
docker build -t myrepo/nginx:latest .

cd ../wordpress
docker build -t myrepo/wordpress:latest .
3. Deploy with Helm
Deploy the WordPress application using Helm.

bash
Copy code
helm install my-release ./wordpress-chart
Usage
Accessing WordPress
To access WordPress, retrieve the URL using Minikube:

bash
Copy code
minikube service my-release-wordpress-chart --url
Open the provided URL in your web browser to access your WordPress site.

Cleaning Up
To delete the deployment:

bash
Copy code
helm delete my-release
Contributing
Contributions are welcome! Please fork the repository and create a pull request with your changes.

License
This project is licensed under the MIT License.

