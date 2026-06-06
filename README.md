# Smart Automation Engine

A comprehensive Spring Boot-based workflow automation engine that processes BPMN XML data and manages workflow configurations with enterprise-grade features.

## Features

- **JWT Authentication**: Secure API access with token-based authentication
- **RESTful APIs**: Complete CRUD operations for workflow management
- **Database Migrations**: Flyway-based schema management
- **Redis Caching**: Performance optimization with Redis cache
- **Docker Support**: Containerized deployment with Docker Compose
- **API Documentation**: OpenAPI/Swagger documentation
- **Monitoring**: Actuator endpoints for health checks and metrics
- **Error Handling**: Global exception handling with structured responses

## Technology Stack

- **Java 17**
- **Spring Boot 4.0.5**
- **Spring Security** (JWT Authentication)
- **Spring Data JPA** (MySQL)
- **Flyway** (Database Migrations)
- **Redis** (Caching)
- **OpenAPI** (API Documentation)
- **Docker** (Containerization)
- **Maven** (Build Tool)

## Quick Start

### Prerequisites

- Java 17+
- Maven 3.8+
- MySQL 8.0+
- Redis 7.0+

### Local Development

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd SmartAutomationEngine
   ```

2. **Configure Database**
   ```bash
   mysql -u root -p
   CREATE DATABASE smart_automation_engine;
   ```

3. **Update Configuration**
   Update `src/main/resources/application.yml` with your database and Redis credentials.

4. **Run the Application**
   ```bash
   mvn spring-boot:run
   ```

The application will be available at `http://localhost:8080/SmartAutomationEngine`

### Docker Deployment

1. **Build and Run with Docker Compose**
   ```bash
   docker-compose up -d
   ```

2. **Access the Application**
   - API: `http://localhost:8080/SmartAutomationEngine`
   - Swagger UI: `http://localhost:8080/SmartAutomationEngine/swagger-ui.html`
   - Health Check: `http://localhost:8080/SmartAutomationEngine/actuator/health`

## API Documentation

### Authentication

#### Login
```bash
curl -X POST http://localhost:8080/SmartAutomationEngine/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"admin123"}'
```

#### Validate Token
```bash
curl -X POST http://localhost:8080/SmartAutomationEngine/api/v1/auth/validate \
  -H "Authorization: Bearer <jwt-token>"
```

### Workflow Management

#### Upload Workflows
```bash
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
```

#### Get Workflow by Code
```bash
curl -X GET "http://localhost:8080/SmartAutomationEngine/api/v1/workflows/WF001?tenantId=tenant1" \
  -H "Authorization: Bearer <jwt-token>"
```

#### Get Workflows by Tenant
```bash
curl -X GET http://localhost:8080/SmartAutomationEngine/api/v1/workflows/tenant/tenant1 \
  -H "Authorization: Bearer <jwt-token>"
```

#### Delete Workflow
```bash
curl -X DELETE "http://localhost:8080/SmartAutomationEngine/api/v1/workflows/WF001?tenantId=tenant1" \
  -H "Authorization: Bearer <jwt-token>"
```

## Configuration

### Application Configuration

Key configuration properties in `application.yml`:

```yaml
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
```

### Environment Variables

The application supports the following environment variables:

- `DATABASE_URL`: Database connection URL
- `DATABASE_USERNAME`: Database username
- `DATABASE_PASSWORD`: Database password
- `REDIS_HOST`: Redis server host
- `REDIS_PORT`: Redis server port
- `JWT_SECRET`: JWT signing secret
- `SERVER_PORT`: Application port

## Default Users

For demonstration purposes, the application includes these default users:

- **Username**: `admin`, **Password**: `admin123`, **Role**: `ADMIN`
- **Username**: `user`, **Password**: `user123`, **Role**: `USER`

## Monitoring

### Health Endpoints

- **Health Check**: `/actuator/health`
- **Application Info**: `/actuator/info`
- **Metrics**: `/actuator/metrics`
- **Prometheus**: `/actuator/prometheus`

### Logging

Application logs are configured to:
- Console output with structured format
- File logging at `logs/smart-automation-engine.log`
- Log rotation with 10MB max file size and 30 days retention

## Development

### Running Tests

```bash
mvn test
```

### Building the Application

```bash
mvn clean package
```

### Code Quality

The project includes:
- Input validation with Jakarta Validation
- Global exception handling
- Structured logging
- Comprehensive API documentation

## Architecture

### Package Structure

```
org.jsp.smartautomationengine/
  config/          # Configuration classes
  controller/      # REST API controllers
  dto/            # Data Transfer Objects
  entity/         # JPA entities
  exception/      # Exception handling
  repository/     # Data access layer
  security/       # Security components
  service/        # Business logic
```

### Key Components

- **WorkFlowController**: REST endpoints for workflow management
- **AuthController**: Authentication and token management
- **WorkFlowService**: Business logic for workflow operations
- **JwtTokenUtil**: JWT token generation and validation
- **GlobalExceptionHandler**: Centralized error handling

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Submit a pull request

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.
