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

# Modernise and Containerise

## Prerequisites

Before starting, ensure you have the following:

- **GitHub account**
- **Azure subscription**
- **GitHub App Modernization extension** installed
- **Docker** installed locally
- **Azure CLI** installed and authenticated
- **VS Code** (recommended)

Basic familiarity with:
- Java & Spring Boot
- Containers
- Kubernetes concepts

---

## Setting up the GitHub Repository

1. Fork this repository
2. Clone it locally:

```bash
git clone https://github.com/<your-org-or-user>/spring-petclinic-appmod-demo.git
cd spring-petclinic-appmod-demo
```

## Overview

Spring Petclinic is a Spring Boot application that demonstrates:

- Layered architecture (controller, service, repository)
- Spring MVC and REST patterns
- Embedded database by default
- Maven‑based build

## Running the Application Locally

- ./mvnw spring
- Access the application at:
http://localhost:8080

### Build and Run as a JAR

./mvnw package
java -jar target/*.jar

## Modernising with GitHub App Modernization

GitHub App Modernization (AppMod) helps assess and modernise applications by:

- Analysing the Java codebase
- Identifying containerisation readiness
- Providing Azure‑aligned modernisation guidance

### In this demo, AppMod is used to:

- Validate the application for container deployment
- Inform platform and runtime decisions
- Guide AKS‑based deployment

```The application code remains largely unchanged to keep the focus on delivery modernisation.```

## Containerisation

The application is containerised using:

- Multi‑stage Docker builds
- Maven build stage
- Lightweight Java runtime image

Key benefits:

- Portable deployment
- Reproducible builds
- Cloud‑native packaging

## Deploying to Azure Kubernetes Service (AKS)

The containerised application is deployed to AKS using:

- Kubernetes Deployment
- Kubernetes Service
- Optional Ingress

### The deployment demonstrates:

- Stateless application design
- Container image pull from ACR
- External access via Kubernetes Service or Ingress


## CI/CD with GitHub Actions

GitHub Actions is used to automate the full CI/CD lifecycle directly from the repository.

### What the Workflow Does

- Builds the Java application
- Builds the Docker image
- Pushes the image to Azure Container Registry
- Deploys the application to AKS

## Database Configuration

By default, Spring Petclinic uses an in‑memory database, which is ideal for:

- Demos
- Workshops
- Labs

This demo intentionally avoids persistent storage to keep the focus on:

- Modernisation
- Containerisation
- Platform deployment

## Cleanup

To avoid Azure costs after the demo:

- Delete the AKS cluster
- Delete the Azure Container Registry
- Remove associated resource groups

## Contributing

This project welcomes contributions.
Most contributions require agreement to a Contributor License Agreement (CLA):
https://cla.opensource.microsoft.com
This project follows the Microsoft Open Source Code of Conduct:
https://opensource.microsoft.com/codeofconduct/

Disclaimer
This repository is intended for demo and educational purposes only and is not a production reference architecture.
