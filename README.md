Skip to content
gauravavailable
Smart-Automation-Engine-1
Repository navigation
Code
Issues
Pull requests
Agents
Actions
Projects
Security and quality
Insights
Owner avatar
Smart-Automation-Engine-1
Public
gauravavailable/Smart-Automation-Engine-1
Name		
author
Gaurav
commit
05298d9
 · 
last month
.mvn/wrapper
commit
3 months ago
src
commit
last month
.dockerignore
commit
last month
.gitattributes
commit
3 months ago
.gitignore
commit
3 months ago
Dockerfile
commit
last month
README.md
commit
last month
docker-compose.yml
commit
last month
mvnw
commit
3 months ago
mvnw.cmd
commit
3 months ago
myapp.log
commit
last month
myapp.log.2026-04-21.0.gz
commit
2 months ago
myapp.log.2026-04-22.0.gz
commit
last month
pom.xml
commit
last month
Repository files navigation
README
Smart Automation Engine

A comprehensive Spring Boot-based workflow automation engine that processes BPMN XML data and manages workflow configurations with enterprise-grade features.

Features

JWT Authentication: Secure API access with token-based authentication
RESTful APIs: Complete CRUD operations for workflow management
Database Migrations: Flyway-based schema management
Redis Caching: Performance optimization with Redis cache
Docker Support: Containerized deployment with Docker Compose
API Documentation: OpenAPI/Swagger documentation
Monitoring: Actuator endpoints for health checks and metrics
Error Handling: Global exception handling with structured responses
Technology Stack

Java 17
Spring Boot 4.0.5
Spring Security (JWT Authentication)
Spring Data JPA (MySQL)
Flyway (Database Migrations)
Redis (Caching)
OpenAPI (API Documentation)
Docker (Containerization)
Maven (Build Tool)
Quick Start

Prerequisites

Java 17+
Maven 3.8+
MySQL 8.0+
Redis 7.0+
Local Development

Clone the repository

git clone <repository-url>
cd SmartAutomationEngine
Configure Database

mysql -u root -p
CREATE DATABASE smart_automation_engine;
Update Configuration Update src/main/resources/application.yml with your database and Redis credentials.

Run the Application

mvn spring-boot:run
The application will be available at http://localhost:8080/SmartAutomationEngine

Docker Deployment

Build and Run with Docker Compose

docker-compose up -d
Access the Application

API: http://localhost:8080/SmartAutomationEngine
Swagger UI: http://localhost:8080/SmartAutomationEngine/swagger-ui.html
Health Check: http://localhost:8080/SmartAutomationEngine/actuator/health
API Documentation

Authentication

Login

curl -X POST http://localhost:8080/SmartAutomationEngine/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"admin123"}'
Validate Token

curl -X POST http://localhost:8080/SmartAutomationEngine/api/v1/auth/validate \
  -H "Authorization: Bearer <jwt-token>"
Workflow Management

Upload Workflows

curl -X POST http://localhost:8080/SmartAutomationEngine/api/v1/workflows/upload \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <jwt-token>" \
  -d '[{
    "workflowcode":"WF001",
    "sourcedata":"<bpmn>...</bpmn>",
    "tenantId":"tenant1",
    "workflowname":"Sample Workflow",
    "uniquefield":"id",
    "entitycode":"ENTITY001"
  }]'
Get Workflow by Code

curl -X GET "http://localhost:8080/SmartAutomationEngine/api/v1/workflows/WF001?tenantId=tenant1" \
  -H "Authorization: Bearer <jwt-token>"
Get Workflows by Tenant

curl -X GET http://localhost:8080/SmartAutomationEngine/api/v1/workflows/tenant/tenant1 \
  -H "Authorization: Bearer <jwt-token>"
Delete Workflow

curl -X DELETE "http://localhost:8080/SmartAutomationEngine/api/v1/workflows/WF001?tenantId=tenant1" \
  -H "Authorization: Bearer <jwt-token>"
Configuration

Application Configuration

Key configuration properties in application.yml:

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/smart_automation_engine
    username: root
    password: password
  
  redis:
    host: localhost
    port: 6379
  
  jwt:
    secret: mySecretKey
    expiration: 86400
Environment Variables

The application supports the following environment variables:

DATABASE_URL: Database connection URL
DATABASE_USERNAME: Database username
DATABASE_PASSWORD: Database password
REDIS_HOST: Redis server host
REDIS_PORT: Redis server port
JWT_SECRET: JWT signing secret
SERVER_PORT: Application port
Default Users

For demonstration purposes, the application includes these default users:

Username: admin, Password: admin123, Role: ADMIN
Username: user, Password: user123, Role: USER
Monitoring

Health Endpoints

Health Check: /actuator/health
Application Info: /actuator/info
Metrics: /actuator/metrics
Prometheus: /actuator/prometheus
Logging

Application logs are configured to:

Console output with structured format
File logging at logs/smart-automation-engine.log
Log rotation with 10MB max file size and 30 days retention
Development

Running Tests

mvn test
Building the Application

mvn clean package
Code Quality

The project includes:

Input validation with Jakarta Validation
Global exception handling
Structured logging
Comprehensive API documentation
Architecture

Package Structure

org.jsp.smartautomationengine/
  config/          # Configuration classes
  controller/      # REST API controllers
  dto/            # Data Transfer Objects
  entity/         # JPA entities
  exception/      # Exception handling
  repository/     # Data access layer
  security/       # Security components
  service/        # Business logic
Key Components

WorkFlowController: REST endpoints for workflow management
AuthController: Authentication and token management
WorkFlowService: Business logic for workflow operations
JwtTokenUtil: JWT token generation and validation
GlobalExceptionHandler: Centralized error handling
Contributing

Fork the repository
Create a feature branch
Make your changes
Add tests for new functionality
Submit a pull request
License

This project is licensed under the Apache License 2.0 - see the LICENSE file for details.
About

Developed a scalable workflow automation engine using Java, Spring Boot, and microservices to manage dynamic business processes with BPMN integration, REST APIs, and efficient database handling using JPA and Hibernate.

Resources
 Readme
 Activity
Stars
 0 stars
Watchers
 0 watching
Forks
 0 forks
Report repository
Releases

No releases published
Packages

No packages published
Contributors

No contributors
Languages

Java
99.1%
Dockerfile
0.9%
Footer
© 2026 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Status
Community
Docs
Contact
Manage cookies
Do not share my personal information
