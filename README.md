# 🚀 Deploy a Web App on Nginx Server Using AWS App Runner

Welcome to this guide! In this tutorial, we will deploy a simple web application on an Nginx server using AWS App Runner. Follow these steps to get your application up and running in no time! 🕒

---

## 📋 Prerequisites

Before you begin, make sure you have the following:

1. **AWS Account** 🔑 - Sign up [here](https://aws.amazon.com/) if you don't have one.
2. **Docker Installed** 🐳 - Download it from [Docker's website](https://www.docker.com/products/docker-desktop).
3. **Nginx Configuration File** 📄 - Ensure you have your Nginx configuration ready.
4. **Web App Code** 💻 - Prepare your application files.
5. **AWS CLI** ⚙️ - Install it by following the instructions [here](https://aws.amazon.com/cli/).

---

## 🛠 Steps to Deploy

### 1️⃣ Create Your Nginx Web App Docker Image

1. Clone or create your web app project:

    ```bash
    git clone https://github.com/rushi2828/deploy-web-app-on-nginx-server-using-aws-app-runner.git
    cd deploy-web-app-on-nginx-server-using-aws-app-runner.git
    ```

2. Create a `Dockerfile` in the root directory of your project:

    ```dockerfile
    FROM --platform=linux/amd64 nginx:latest
    WORKDIR /usr/share/nginx/html
    COPY index.html index.html
    ```

3. Build and test your Docker image locally:

    ```bash
    docker build -t nginx-web-app .
    ```
    ![image](https://github.com/user-attachments/assets/aa543dfe-8796-4970-999f-33c5f00f379c)

    ```
    docker run -p 8080:80 nginx-web-app
    ```

4. Visit `http://localhost:8080` 🌐 to confirm your app is working.
   
   ![image](https://github.com/user-attachments/assets/ce4694e8-a56b-416c-9e7a-61863395c0a8)

---

### 2️⃣ Push Docker Image to AWS Elastic Container Registry (ECR)

1. Authenticate Docker to your AWS ECR:

    ```bash
    aws ecr get-login-password --region <your-region> | docker login --username AWS --password-stdin <your-account-id>.dkr.ecr.<your-region>.amazonaws.com
    ```

2. Create an ECR repository:

    ```bash
    aws ecr create-repository --repository-name nginx-web-app
    ```

3. Tag and push your Docker image:

    ```bash
    docker tag your-nginx-app:latest <your-account-id>.dkr.ecr.<your-region>.amazonaws.com/nginx-web-app:latest
    docker push <your-account-id>.dkr.ecr.<your-region>.amazonaws.com/nginx-web-app:latest
    ```

---

### 3️⃣ Deploy to AWS App Runner

1. Go to the [AWS App Runner Console](https://console.aws.amazon.com/apprunner/home) 🖥️.
2. Select **Create Service**.
3. Choose **Container Registry** as the source and connect to your ECR repository.
4. Configure your service:
   - Set a name for your service (e.g., `nginx-web-app-service`).
   - Select the desired instance size and auto-scaling configuration.
5. Deploy the service and wait for the status to change to **Running**. ✅

---

## 🕵️ Verify the Deployment

1. Go to the App Runner service dashboard.
2. Copy the default domain (e.g., `https://your-service-id.awsapprunner.com`).
3. Paste it into your browser to view your web app live! 🌟

---
