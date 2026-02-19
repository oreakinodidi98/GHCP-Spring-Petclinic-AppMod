---
page_type: sample
description: "Modernise and containerise a Java Spring Petclinic application using GitHub App Modernization and deploy to AKS"
products:
- GitHub App Modernization
- Azure Kubernetes Service
- GitHub Actions
languages:
- Java
urlFragment: https://github.com/spring-projects/spring-petclinic
---

# Spring Petclinic - Application Modernization Demo

> **Transform a traditional Java application into a cloud-native, containerized workload running on Azure Kubernetes Service (AKS)**

---

## What This Repository Is

This repository demonstrates an **end-to-end application modernization journey** using GitHub App Modernization (AppMod). It takes the classic [Spring Petclinic](https://github.com/spring-projects/spring-petclinic) sample application and walks you through:

1. **Analyzing** the codebase for cloud readiness
2. **Containerizing** the application with Docker
3. **Deploying** to Azure Kubernetes Service (AKS)
4. **Automating** the entire pipeline with GitHub Actions

---

## End Goal

By completing this demo, you will achieve:

| Outcome | Description |
|---------|-------------|
| **Containerized Application** | Spring Petclinic packaged as a Docker image |
| **Cloud Deployment** | Application running on AKS with external access |
| **CI/CD Pipeline** | Automated build, push, and deploy via GitHub Actions |
| **Modernization Experience** | Hands-on familiarity with GitHub AppMod tooling |

```
┌─────────────────┐      ┌─────────────────┐      ┌─────────────────┐      ┌─────────────────┐
│  Source Code    │ ──▶  │  Docker Image   │ ──▶  │  Azure ACR      │ ──▶  │  AKS Cluster    │
│  (Spring Boot)  │      │  (Multi-stage)  │      │  (Registry)     │      │  (Production)   │
└─────────────────┘      └─────────────────┘      └─────────────────┘      └─────────────────┘
```

---

## Table of Contents

- [Spring Petclinic - Application Modernization Demo](#spring-petclinic---application-modernization-demo)
  - [What This Repository Is](#what-this-repository-is)
  - [End Goal](#end-goal)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Quick Start](#quick-start)
    - [1. Fork and Clone](#1-fork-and-clone)
    - [2. Build and Run Locally](#2-build-and-run-locally)
    - [3. Start the Application](#3-start-the-application)
    - [4. Access the Application](#4-access-the-application)
  - [About Spring Petclinic](#about-spring-petclinic)
  - [Modernization Workflow](#modernization-workflow)
    - [Step 1: Analyze with GitHub AppMod](#step-1-analyze-with-github-appmod)
    - [Step 2: Containerize](#step-2-containerize)
    - [Step 3: Deploy to AKS](#step-3-deploy-to-aks)
    - [Step 4: Automate with GitHub Actions](#step-4-automate-with-github-actions)
  - [Database Configuration](#database-configuration)
  - [Cleanup](#cleanup)
  - [Contributing](#contributing)
  - [Disclaimer](#disclaimer)

---

## Prerequisites

| Requirement | Purpose |
|-------------|---------|
| **GitHub Account** | Source control and Actions |
| **Azure Subscription** | AKS and ACR hosting |
| **GitHub App Modernization Extension** | Analysis and guidance |
| **Docker** | Local container builds |
| **Azure CLI** | Azure resource management |
| **VS Code** (recommended) | Development environment |

**Recommended Knowledge:**
- Java & Spring Boot basics
- Container fundamentals
- Kubernetes concepts (Pods, Deployments, Services)

---

## Quick Start

### 1. Fork and Clone

```bash
git clone https://github.com/<your-username>/spring-petclinic-appmod-demo.git
cd spring-petclinic-appmod-demo
```

### 2. Build and Run Locally

```bash
# Set Java environment (Windows PowerShell)
$env:JAVA_HOME = "C:\Program Files\Java\jdk-17.0.18"

# Apply code formatting
./mvnw spring-javaformat:apply -q

# Compile the project
./mvnw clean compile --strict-checksums

# Run all tests
./mvnw test --strict-checksums

# Run tests (excluding database integration tests)
./mvnw test -Dtest='!PostgresIntegrationTests,!MySqlIntegrationTests'

# Package the application
./mvnw package -DskipTests --strict-checksums
```

### 3. Start the Application

```bash
# Run on default port (8080)
./mvnw spring-boot:run

# Or specify a custom port
./mvnw spring-boot:run '-Dspring-boot.run.arguments=--server.port=8081'
```

### 4. Access the Application

Once running, open your browser to: **http://localhost:8080**

---

## About Spring Petclinic

Spring Petclinic is a classic sample application demonstrating Spring Boot best practices:

| Feature | Technology |
|---------|------------|
| **Architecture** | Layered (Controller → Service → Repository) |
| **Web Framework** | Spring MVC with Thymeleaf templates |
| **Data Access** | Spring Data JPA |
| **Database** | HSQLDB (in-memory, default) or MySQL |
| **Build Tool** | Maven |

---

## Modernization Workflow

### Step 1: Analyze with GitHub AppMod

GitHub App Modernization assesses your codebase and provides:

- **Containerization readiness** analysis
- **Azure-aligned recommendations** for target platforms
- **Migration guidance** for cloud deployment

> The application code remains largely unchanged—the focus is on *delivery modernization*, not code refactoring.

### Step 2: Containerize

The application uses a **multi-stage Docker build**:

```dockerfile
# Stage 1: Build
FROM maven:3.9-eclipse-temurin-17 AS build
COPY . .
RUN mvn package -DskipTests

# Stage 2: Runtime
FROM eclipse-temurin:17-jre-alpine
COPY --from=build /target/*.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]
```

**Benefits:**
- Portable and reproducible builds
- Smaller runtime image
- Cloud-native packaging

### Step 3: Deploy to AKS

Deploy to Azure Kubernetes Service using:

| Resource | Purpose |
|----------|---------|
| **Deployment** | Manages application Pods |
| **Service** | Exposes the app (LoadBalancer or ClusterIP) |
| **Ingress** (optional) | HTTP routing and TLS termination |

**Key Design Decisions:**
- Stateless application design (no persistent volumes)
- Images pulled from Azure Container Registry (ACR)
- External access via Service or Ingress

### Step 4: Automate with GitHub Actions

The CI/CD pipeline automates:

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  Build JAR   │ ─▶ │ Build Image  │ ─▶ │ Push to ACR  │ ─▶ │ Deploy AKS   │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
```

- Triggered on push to `main`
- Builds and tests the Java application
- Builds and tags the Docker image
- Pushes to Azure Container Registry
- Deploys to AKS cluster

---

## Database Configuration

| Mode | Database | Use Case |
|------|----------|----------|
| **Default** | HSQLDB (in-memory) | Demos, workshops, quick testing |
| **Production** | MySQL | Persistent data requirements |

This demo uses the **in-memory database** to keep focus on:
- Modernization process
- Containerization techniques
- Platform deployment patterns

---

## Cleanup

To avoid ongoing Azure costs after completing the demo:

```bash
# Delete the resource group (removes AKS, ACR, and related resources)
az group delete --name <your-resource-group> --yes --no-wait
```

---

## Contributing

This project welcomes contributions and suggestions.

- **CLA**: Most contributions require a [Contributor License Agreement](https://cla.opensource.microsoft.com)
- **Code of Conduct**: This project follows the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/)

---

## Disclaimer

> This repository is intended for **demo and educational purposes only** and is not a production reference architecture.
