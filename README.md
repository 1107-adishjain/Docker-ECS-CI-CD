# ECS CI/CD Pipeline with Jenkins

This repository contains a **Jenkins Declarative Pipeline** (`Jenkinsfile`) that automates the complete CI/CD workflow for a Java application using Maven, Docker, AWS ECR, and AWS ECS.

---

## 🚀 Features

- **Code Checkout** from a Git repository.
- **Build & Package** Java application using Maven.
- **Run Unit Tests** to ensure code quality.
- **Static Code Analysis** with Checkstyle and SonarQube.
- **Quality Gate Check** via SonarQube before deployment.
- **Docker Image Build** using a multi-stage Dockerfile.
- **Push Image** to AWS Elastic Container Registry (ECR).
- **Deploy to AWS ECS** with a rolling update strategy.
- **Slack Notifications** for build results.

---

## 🛠 Technologies Used

- **Jenkins Declarative Pipeline**
- **Apache Maven** for build and dependency management
- **Java 17**
- **SonarQube** for code analysis
- **Docker** for containerization
- **AWS ECR** for container image storage
- **AWS ECS** for container orchestration
- **Slack** for build status notifications

---

## 📦 Pipeline Stages

1. **Fetch Code**  
   Clones the application source code from a specified Git branch.

2. **Build**  
   Compiles and packages the application, producing a `.war` file.

3. **Unit Test**  
   Executes automated tests to validate code functionality.

4. **Checkstyle Analysis**  
   Runs Checkstyle to enforce coding standards.

5. **Sonar Code Analysis**  
   Sends code quality metrics to SonarQube.

6. **Quality Gate**  
   Waits for SonarQube quality gate approval before continuing.

7. **Building Image**  
   Builds a Docker image using a multi-stage Dockerfile.

8. **Push Image to ECR**  
   Pushes the built image to AWS ECR.

9. **Remove Image from Jenkins**  
   Removes the local Docker image to free up space.

10. **Deploy to ECS**  
    Forces ECS to pull the latest image and update running tasks.

---

## 📋 Prerequisites

Before running the pipeline, ensure you have:

- **Jenkins** with the following plugins:
  - Pipeline
  - Git
  - Docker Pipeline
  - AWS Credentials
  - SonarQube Scanner
  - Slack Notification
- **AWS CLI** installed and configured on the Jenkins agent.
- **ECR Repository** created in AWS.
- **ECS Cluster** and **Service** configured.
- Valid **AWS Credentials** stored in Jenkins (`awscreds`).
- Configured **SonarQube Server** in Jenkins (`sonar-server`).
- Configured **Slack Webhook** in Jenkins.

---

## ⚙️ Environment Variables in Jenkinsfile

| Variable             | Description                                   |
|----------------------|-----------------------------------------------|
| `registry`           | AWS ECR repository URL                        |
| `registryCredential` | Jenkins credential ID for AWS                 |
| `dockerImage`        | Holds Docker image reference during build     |
| `clusterName`        | AWS ECS Cluster name                          |
| `serviceName`        | AWS ECS Service name                          |

---

## ▶️ How to Run

1. Clone this repository.  
2. In Jenkins, create a new **Pipeline** job.  
3. Set the pipeline to fetch the `Jenkinsfile` from this repository.  
4. Update variables (`registry`, `clusterName`, `serviceName`) as per your AWS setup.  
5. Run the pipeline.

---

## 📢 Notifications

The pipeline sends **Slack notifications** after every run with:

- Build status
- Job name
- Build number
- Link to console logs

---

## 📊 Pipeline Flow Diagram

![Pipeline Flow](ecs_cicd_pipeline_flow.png)
