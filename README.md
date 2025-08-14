# Java Maven Web Application

A simple Java web application built to gain hands-on experience with CI/CD pipeline automation.

## What I Built

- Simple Java web application with JSP pages
- Maven configuration for build management
- Dockerfile for containerization
- Complete Jenkins CI/CD pipeline

## Technologies I Learned

- Java web development
- Maven build automation
- Docker containerization
- Jenkins pipeline creation
- CI/CD automation concepts

## Application Structure

```
src/main/webapp/
├── index.jsp          # Main landing page
├── demo.jsp           
└── WEB-INF/web.xml    
```

## Build & Run

```bash
mvn clean package
```

This creates a deployable WAR file in the `target/` directory that can be deployed to Tomcat or containerized with Docker.

## CI/CD Pipeline Experience

### What I Used
- Jenkins on EC2 instance
- Docker on EC2 instance

### Pipeline Implementation
1. Jenkins dashboard access at `http://your-ec2-ip:8080`
2. Required plugins installed:
   - Maven Integration Plugin
   - Docker Pipeline Plugin
   - GitHub Integration Plugin

3. Created Pipeline job using the `Jenkinsfile` in this repository

4. The `Jenkinsfile` contains the complete pipeline configuration for:
   - Building the Maven project
   - Creating Docker image
   - Pushing to Docker Hub
   - Deploying the container

Application runs at: `http://your-ec2-ip:9000/<your-app-name>`