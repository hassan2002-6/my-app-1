# AWS Containerized Web Application (Next.js)

This project demonstrates a fully automated containerization and deployment pipeline using AWS-native services, serving as an alternative to the Azure Containerization assignment.

## Architecture

```text
GitHub Repository
      |
      v
GitHub Actions Pipeline (Build & Push)
      |
      v
Amazon ECR (Private Container Registry)
      |
      v
AWS App Runner (Managed Container Hosting)
      |
      v
Public Web URL (HTTPS)
```

## AWS Service Mapping

| Azure Service                    | AWS Equivalent                    |
| -------------------------------- | --------------------------------- |
| Azure Container Registry (ACR)   | Amazon ECR                        |
| Azure DevOps Pipelines           | GitHub Actions                    |
| Azure App Service for Containers | AWS App Runner                    |
| Azure Monitor / Log Analytics    | Amazon CloudWatch                 |

## Deployment Features

- **Multi-stage Docker Build**: Optimized image size and security using `node:20-alpine` and non-root users.
- **Automated CI/CD**: Pushing to the `main` branch triggers a GitHub Actions workflow that builds, tags, and pushes the image to Amazon ECR.
- **Continuous Deployment**: AWS App Runner is configured to automatically redeploy whenever a new image tag (`latest`) is pushed to ECR.
- **Health Monitoring**: Integrated health checks and CloudWatch logging.

## Local Development & Docker

### Build Image Locally
```bash
docker build -t my-app-1 .
```

### Run Locally
```bash
docker run -p 3000:3000 my-app-1
```

## How to View Logs

Application logs and deployment logs are centrally managed in **Amazon CloudWatch**.
1. Open the [AWS App Runner Console](https://console.aws.amazon.com/apprunner/).
2. Select the `my-app-1` service.
3. Go to the **Logs** tab to view:
   - **Service logs**: Deployment and scaling events.
   - **Application logs**: Stdout/stderr from your container.

## Live Application
**URL:** [https://thjnsgjnu5.us-east-1.awsapprunner.com](https://thjnsgjnu5.us-east-1.awsapprunner.com)
