# Intelligent Enterprise Operations & Decision Platform (IEODP)

[![Java](https://img.shields.io/badge/Java-17+-blue.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-4.0.1-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![License](https://img.shields.io/badge/License-Proprietary-red.svg)](LICENSE)

---

## Project Owner Information

- **Name**: Bathygari Pavan  
- **Employee ID**: PIPL0583  
- **Domain**: Java Backend Development

---

## Overview

**Intelligent Enterprise Operations & Decision Platform (IEODP)** is a production-grade, enterprise-ready Java backend system built with Spring Boot. It provides a comprehensive solution for workflow management, user administration, audit logging, and seamless integration with Python/AI services.

### Key Features

- 🔐 **JWT Authentication with Refresh Tokens**: Secure, stateless authentication with token rotation
- 👥 **Role-Based Access Control (RBAC)**: Fine-grained permissions system with 4 predefined roles
- 🔄 **Workflow State Machine**: Business process management with configurable state transitions
- 📊 **Comprehensive Audit Logging**: Full traceability, compliance, and correlation ID tracking
- 🌐 **RESTful API**: Versioned APIs (`/api/v1/`) with OpenAPI/Swagger documentation
- 📈 **Enterprise Data Handling**: Pagination, sorting, filtering, and optimized JPA queries
- 🐍 **Python Service Integration**: Seamless integration with Python FastAPI services for AI/ML operations
- 🔗 **External System Integration**: Ready for integration with frontend apps, microservices, and analytics tools
- ⚡ **Performance Optimized**: Connection pooling, query optimization, and strategic indexing

## Technology Stack

### Core Framework
- **Java 17+** - Modern Java with records, pattern matching, and enhanced performance
- **Spring Boot 4.0.1** - Enterprise framework for building production-ready applications
- **Spring Security** - Comprehensive security framework with JWT support
- **Spring Data JPA** - Data access layer with repository pattern
- **Maven** - Dependency management and build automation

### Database
- **MySQL 8.0+** or **PostgreSQL 12+** - Relational database support
- **HikariCP** - High-performance JDBC connection pooling
- **JPA/Hibernate** - Object-relational mapping

### API Documentation
- **OpenAPI 3.0** / **Swagger UI** - Interactive API documentation
- **SpringDoc OpenAPI** - Automatic API documentation generation

### Security
- **JWT (JSON Web Tokens)** - Stateless authentication
- **BCrypt** - Password hashing
- **Spring Method Security** - Method-level authorization

### Utilities
- **Lombok** - Reduces boilerplate code
- **Jakarta Validation** - Input validation framework

### Integration
- **RestTemplate** - HTTP client for Python service integration
- **Jackson** - JSON serialization/deserialization

## Project Architecture

The project follows **Layered Architecture** with **Domain-Driven Design (DDD)** principles:

```
com.company.platform
├── config              # Configuration classes
│   ├── security        # Security configuration (SecurityConfig, MethodSecurityConfig)
│   ├── swagger         # API documentation (SwaggerConfig)
│   ├── DataInitializer.java    # Database initialization
│   ├── JpaAuditingConfig.java  # JPA auditing configuration
│   └── WebConfig.java          # Web configuration
├── common              # Shared components
│   ├── domain          # Base entities (BaseEntity)
│   ├── exception       # Custom exceptions (BusinessException, NotFoundException, etc.)
│   ├── interceptor     # HTTP interceptors (ApiVersionInterceptor)
│   ├── response        # Standardized responses (ApiResponse, ErrorResponse)
│   └── util            # Utility classes (CorrelationIdUtil)
├── security            # Security components
│   ├── jwt             # JWT implementation (JwtService, JwtAuthenticationFilter)
│   └── service         # Security services (CustomUserDetailsService)
├── auth                # Authentication module
│   ├── controller      # REST controllers (AuthController)
│   ├── dto             # Data transfer objects (AuthResponse, LoginRequest, RegisterRequest)
│   └── service         # Business logic (AuthService)
├── users               # User management module
│   ├── controller      # REST controllers (UserController)
│   ├── domain          # Domain entities (User, Role, Permission, RefreshToken)
│   ├── dto             # Data transfer objects (UserDTO)
│   ├── repository      # Data access (UserRepository, RoleRepository, etc.)
│   └── service         # Business logic (UserService)
├── workflows           # Workflow management module
│   ├── controller      # REST controllers (WorkflowController)
│   ├── domain          # Domain entities (WorkflowItem, WorkflowState, WorkflowAction)
│   ├── dto             # Data transfer objects (WorkflowRequest, WorkflowResponse)
│   ├── repository      # Data access (WorkflowItemRepository)
│   └── service         # Business logic (WorkflowService, WorkflowEngine, WorkflowIntegrationService)
├── audit               # Audit logging module
│   ├── controller      # REST controllers (AuditController)
│   ├── domain          # Domain entities (AuditLog, AuditAction)
│   ├── dto             # Data transfer objects (AuditLogResponse, AuditFilterRequest)
│   ├── repository      # Data access (AuditLogRepository)
│   └── service         # Business logic (AuditService)
├── python              # Python service integration module
│   ├── client          # HTTP client (PythonServiceClient)
│   ├── config          # Configuration (PythonServiceConfig, RestTemplateConfig)
│   ├── controller      # REST controllers (PythonServiceController)
│   ├── dto             # Data transfer objects (AnomalyRequest, RiskRequest, etc.)
│   └── service         # Business logic (PythonServiceIntegrationService)
├── integration         # Integration module for external systems
│   ├── controller      # REST controllers (IntegrationController)
│   └── dto             # Data transfer objects (HealthCheckResponse, IntegrationStatusResponse)
└── PlatformApplication.java    # Main application class
```

## Features

### Authentication & Authorization

- **JWT-based authentication** with access and refresh tokens
- **Token expiration handling** with automatic refresh
- **Four roles**: Admin, Manager, Reviewer, Viewer
- **Permission-based access control** at method level using `@PreAuthorize`
- **Secure password encoding** using BCrypt

### Workflow Engine

State-driven workflow with the following states:
- **CREATED** → **REVIEWED** → **APPROVED** / **REJECTED** → **REOPENED**

**Business Rules:**
- Role-based transition validation
- State machine logic enforcement
- Full audit trail for each transition
- Business rule validation per state

### Audit Logging

- **Comprehensive audit trail** for all significant actions
- **Correlation IDs** for request tracing
- **Entity-level tracking** with before/after values
- **IP address and user agent** logging
- **Searchable audit logs** with filtering

### Data Handling

- **Server-side pagination** with Spring Data
- **Sorting and filtering** support
- **Optimized JPA queries** with JOIN FETCH to avoid N+1
- **Database indexing** strategy for performance
- **Transaction management** with proper rollback

### Error Handling

- **Global exception handler** for consistent error responses
- **Standardized error format** with error codes
- **Validation error reporting** with field-level details
- **Proper HTTP status codes**

## API Documentation

Once the application is running, access Swagger UI at:
- **Swagger UI**: http://localhost:8080/swagger-ui.html
- **OpenAPI JSON**: http://localhost:8080/v3/api-docs

## Getting Started

### Prerequisites

- Java 17 or higher
- Maven 3.6+
- MySQL 8.0+ or PostgreSQL 12+

### Database Setup

1. Create database:
```sql
CREATE DATABASE ieodp_db1;
```

2. Update `application.yaml` with your database credentials:
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/ieodp_db1
    username: your_username
    password: your_password
```

### Running the Application

1. Build the project:
```bash
mvn clean install
```

2. Run the application:
```bash
mvn spring-boot:run
```

3. The application will start on `http://localhost:8080`

### Default Credentials

On first startup, a default admin user is automatically created:
- **Username**: `admin`
- **Password**: `admin123`
- **Role**: `Admin`
- **Email**: `admin@ieodp.com`

> **⚠️ Security Note**: Change the default admin password immediately in production environments.

## API Endpoints

### Authentication (`/api/v1/auth`)

All authentication endpoints are **public** (no authentication required).

| Method | Endpoint | Description | Request Body |
|--------|----------|-------------|--------------|
| `POST` | `/api/v1/auth/register` | Register a new user account | `RegisterRequest` |
| `POST` | `/api/v1/auth/login` | User login (returns JWT tokens) | `LoginRequest` |
| `POST` | `/api/v1/auth/refresh` | Refresh access token | `RefreshTokenRequest` |
| `POST` | `/api/v1/auth/logout` | Logout (revoke refresh token) | `RefreshTokenRequest` |

### Users (`/api/v1/users`)

All endpoints require authentication. Most endpoints require **Manager** or **Admin** role.

| Method | Endpoint | Description | Required Role |
|--------|----------|-------------|---------------|
| `GET` | `/api/v1/users` | Get all users (paginated) | Manager, Admin |
| `GET` | `/api/v1/users/{id}` | Get user by ID | Any authenticated user |
| `GET` | `/api/v1/users/search` | Search users by username, email, name | Manager, Admin |
| `GET` | `/api/v1/users/role/{roleName}` | Get users by role | Manager, Admin |
| `PUT` | `/api/v1/users/{id}` | Update user | Manager, Admin |
| `DELETE` | `/api/v1/users/{id}` | Delete user | Admin only |

### Workflows (`/api/v1/workflows`)

All endpoints require authentication. Permission-based access control is enforced.

| Method | Endpoint | Description | Required Permission |
|--------|----------|-------------|---------------------|
| `POST` | `/api/v1/workflows` | Create new workflow | `WORKFLOW_CREATE` |
| `GET` | `/api/v1/workflows/{id}` | Get workflow by ID | `WORKFLOW_READ` |
| `GET` | `/api/v1/workflows` | Get all workflows (paginated) | `WORKFLOW_READ` |
| `GET` | `/api/v1/workflows/search` | Search workflows with filters | `WORKFLOW_READ` |
| `PUT` | `/api/v1/workflows/{id}` | Update workflow | `WORKFLOW_UPDATE` |
| `POST` | `/api/v1/workflows/{id}/transition` | Transition workflow state | `WORKFLOW_APPROVE`, `WORKFLOW_REJECT`, etc. |
| `POST` | `/api/v1/workflows/{workflowName}/trigger` | Trigger workflow by name | `WORKFLOW_CREATE` |
| `DELETE` | `/api/v1/workflows/{id}` | Delete workflow | `WORKFLOW_DELETE` |

### Audit (`/api/v1/audit`)

All endpoints require authentication. **Reviewer**, **Manager**, or **Admin** role required.

| Method | Endpoint | Description | Required Role |
|--------|----------|-------------|---------------|
| `GET` | `/api/v1/audit` | Get audit logs (paginated, filtered) | Reviewer, Manager, Admin |
| `GET` | `/api/v1/audit/entity/{entityType}/{entityId}` | Get audit logs for specific entity | Reviewer, Admin |

### Python Service Integration (`/api/v1/python`)

All endpoints require authentication. These endpoints call Python FastAPI service internally.

| Method | Endpoint | Description | Python Service Endpoint |
|--------|----------|-------------|------------------------|
| `POST` | `/api/v1/python/anomaly/detect` | Detect anomalies in metrics | `/anomaly/detect` |
| `POST` | `/api/v1/python/risk/evaluate` | Evaluate risk levels | `/risk/evaluate` |
| `POST` | `/api/v1/python/decision/evaluate` | Evaluate decisions | `/decision/evaluate` |
| `POST` | `/api/v1/python/ingestion/process` | Process data ingestion | `/ingestion/process` |
| `GET` | `/api/v1/python/health` | Python service health check | `/health/health` |

### Integration (`/api/v1/integration`)

Endpoints for external system integration. All endpoints require authentication.

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/v1/integration/health` | Integration health check |
| `POST` | `/api/v1/integration/workflows/trigger` | Trigger workflow from external system |

> **Note**: For detailed API documentation with request/response examples, see:
> - [Java Backend APIs.md](Java%20Backend%20APIs.md) - Complete API reference with examples
> - [Testing APIs.md](Testing%20APIs.md) - Testing guide and examples
> - Swagger UI: http://localhost:8080/swagger-ui.html (when application is running)

## Security Model

### Roles & Permissions

The system implements a **Role-Based Access Control (RBAC)** model with four predefined roles:

| Role | Description | Key Capabilities |
|------|-------------|------------------|
| **Viewer** | Basic user role | Create and update workflows, submit workflows for review, reopen rejected workflows |
| **Manager** | Management role | All Viewer capabilities, plus: review workflows, approve/reject workflows, manage users, view audit logs |
| **Reviewer** | Audit specialist | Read-only access to audit logs, view workflows, cannot modify data |
| **Admin** | System administrator | Full access to all features, manage all users, delete workflows, view all audit logs |

### Permissions

Permissions are assigned to roles, not directly to users. Key permission types include:

**Workflow Permissions:**
- `WORKFLOW_CREATE` - Create new workflows
- `WORKFLOW_READ` - Read/view workflows
- `WORKFLOW_UPDATE` - Update existing workflows
- `WORKFLOW_DELETE` - Delete workflows (Admin only)
- `WORKFLOW_REVIEW` - Review workflows
- `WORKFLOW_APPROVE` - Approve workflows
- `WORKFLOW_REJECT` - Reject workflows
- `WORKFLOW_REOPEN` - Reopen rejected workflows

**User Management Permissions:**
- `USER_CREATE` - Create users
- `USER_READ` - Read/view users
- `USER_UPDATE` - Update users
- `USER_DELETE` - Delete users (Admin only)

**Audit Permissions:**
- `AUDIT_READ` - Read audit logs
- `AUDIT_EXPORT` - Export audit logs (future feature)

## Workflow State Machine

### State Transitions

```
CREATED --[SUBMIT/REVIEW]--> REVIEWED
REVIEWED --[APPROVE]--> APPROVED
REVIEWED --[REJECT]--> REJECTED
APPROVED --[REJECT]--> REJECTED (Admin only)
REJECTED --[REOPEN]--> REOPENED
REOPENED --[SUBMIT]--> CREATED
```

### Role-Based Transitions

- **CREATED → REVIEWED**: Viewer, Manager
- **REVIEWED → APPROVED**: Manager, Admin
- **REVIEWED → REJECTED**: Manager, Admin
- **APPROVED → REJECTED**: Admin only
- **REJECTED → REOPENED**: Viewer, Manager
- **REOPENED → CREATED**: Viewer

## Transaction Management

Transactions are used strategically:

- **Service methods** marked with `@Transactional` for business operations
- **Read-only transactions** for queries (`@Transactional(readOnly = true)`)
- **Rollback on exceptions** - all exceptions trigger rollback
- **Audit logging** is transactional to ensure logs are never lost

## Logging Strategy

- **Structured logging** with correlation IDs
- **Log levels**: DEBUG for development, INFO for production
- **Correlation IDs** enable request tracing across services
- **File logging** with rotation (10MB, 30 days retention)

# Java Backend APIs

## Base URL
```
http://localhost:8080
```

## Authentication

All endpoints (except auth endpoints) require JWT Bearer token authentication:
```
Authorization: Bearer <your_access_token>
```

**Get Token:**
```bash
POST /api/v1/auth/login
{
  "username": "admin",
  "password": "admin123"
}
```

## Authentication Endpoints

### 1. Register User
**POST** `/api/v1/auth/register`

**Request:**
```json
{
  "username": "john_doe",
  "email": "john.doe@example.com",
  "password": "SecurePass123",
  "firstName": "John",
  "lastName": "Doe",
  "role": "Viewer"
}
```

**Valid Roles:** `Admin`, `Manager`, `Reviewer`, `Viewer`

**Response (201 Created):**
```json
{
  "success": true,
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "tokenType": "Bearer",
    "expiresIn": 3600,
    "username": "john_doe",
    "role": "Viewer",
    "issuedAt": "2026-01-10T20:00:00"
  },
  "message": "User registered successfully"
}
```

### 2. Login
**POST** `/api/v1/auth/login`

**Request:**
```json
{
  "username": "admin",
  "password": "admin123"
}
```

**Response (200 OK):**
```json
{
  "success": true,
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "tokenType": "Bearer",
    "expiresIn": 3600,
    "username": "admin",
    "role": "Admin"
  },
  "message": "Login successful"
}
```

### 3. Refresh Token
**POST** `/api/v1/auth/refresh`

**Request:**
```json
{
  "refreshToken": "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
}
```

### 4. Logout
**POST** `/api/v1/auth/logout`

**Request:**
```json
{
  "refreshToken": "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
}
```

## User Management Endpoints

**Required Roles:** Manager or Admin (except GET by ID)

### 1. Get All Users
**GET** `/api/v1/users?page=0&size=20&sort=createdAt`

**Query Parameters:**
- `page` (optional, default: 0) - Page number
- `size` (optional, default: 20) - Page size
- `sort` (optional, default: createdAt) - Sort field

**Response (200 OK):**
```json
{
  "success": true,
  "data": {
    "content": [
      {
        "id": 1,
        "username": "admin",
        "email": "admin@ieodp.com",
        "firstName": "Admin",
        "lastName": "User",
        "role": "Admin",
        "enabled": true,
        "createdAt": "2026-01-10T10:00:00"
      }
    ],
    "totalElements": 1,
    "totalPages": 1
  }
}
```

### 2. Get User by ID
**GET** `/api/v1/users/{id}`

### 3. Search Users
**GET** `/api/v1/users/search?search=john&page=0&size=20`

### 4. Get Users by Role
**GET** `/api/v1/users/role/{roleName}?page=0&size=20`

### 5. Update User
**PUT** `/api/v1/users/{id}`

**Request:**
```json
{
  "email": "john.updated@example.com",
  "firstName": "John",
  "lastName": "Updated",
  "role": "Manager",
  "enabled": true
}
```

### 6. Delete User
**DELETE** `/api/v1/users/{id}`

**Required Role:** Admin only

## Workflow Management Endpoints

### 1. Create Workflow
**POST** `/api/v1/workflows`

**Request:**
```json
{
  "title": "Process Payment Request",
  "description": "Review and approve payment request for vendor invoice",
  "priority": "HIGH",
  "category": "Finance",
  "assignedToId": 1
}
```

**Priority Values:** `LOW`, `MEDIUM`, `HIGH`, `CRITICAL`

**Response (201 Created):**
```json
{
  "success": true,
  "data": {
    "id": 1,
    "title": "Process Payment Request",
    "description": "Review and approve payment request for vendor invoice",
    "state": "CREATED",
    "priority": "HIGH",
    "category": "Finance",
    "createdBy": {
      "id": 1,
      "username": "admin"
    },
    "assignedTo": {
      "id": 1,
      "username": "admin"
    },
    "createdAt": "2026-01-10T20:00:00"
  },
  "message": "Workflow created successfully"
}
```

### 2. Get Workflow by ID
**GET** `/api/v1/workflows/{id}`

**Response (200 OK):**
```json
{
  "success": true,
  "data": {
    "id": 1,
    "title": "Process Payment Request",
    "description": "Review and approve payment request",
    "state": "CREATED",
    "priority": "HIGH",
    "category": "Finance",
    "createdBy": {
      "id": 1,
      "username": "admin"
    },
    "assignedTo": {
      "id": 2,
      "username": "manager1"
    },
    "createdAt": "2026-01-10T20:00:00",
    "updatedAt": "2026-01-10T20:00:00"
  }
}
```

### 3. Get All Workflows
**GET** `/api/v1/workflows?page=0&size=20&sort=createdAt`

**Query Parameters:**
- `page` (optional, default: 0)
- `size` (optional, default: 20)
- `sort` (optional, default: createdAt)

### 4. Search Workflows
**GET** `/api/v1/workflows/search?search=payment&state=CREATED&page=0&size=20`

**Query Parameters:**
- `search` (optional) - Search term
- `state` (optional) - Filter by state: `CREATED`, `REVIEWED`, `APPROVED`, `REJECTED`, `REOPENED`
- `priority` (optional) - Filter by priority
- `category` (optional) - Filter by category
- `fromDate` (optional) - Filter from date (ISO 8601)
- `toDate` (optional) - Filter to date (ISO 8601)
- `page` (optional, default: 0)
- `size` (optional, default: 20)
- `sort` (optional, default: createdAt,DESC)

### 5. Update Workflow
**PUT** `/api/v1/workflows/{id}`

**Request:**
```json
{
  "title": "Updated Payment Request",
  "description": "Updated description",
  "priority": "CRITICAL",
  "category": "Finance",
  "assignedToId": 1,
  "comments": "Urgent payment required"
}
```

### 6. Transition Workflow State
**POST** `/api/v1/workflows/{id}/transition`

**Request:**
```json
{
  "action": "SUBMIT",
  "comments": "Ready for review"
}
```

**Valid Actions:** `SUBMIT`, `REVIEW`, `APPROVE`, `REJECT`, `REOPEN`

**State Transitions:**
- `CREATED` → `REVIEWED` (SUBMIT by Viewer/Manager, REVIEW by Manager)
- `REVIEWED` → `APPROVED` (APPROVE by Manager/Admin)
- `REVIEWED` → `REJECTED` (REJECT by Manager/Admin)
- `APPROVED` → `REJECTED` (REJECT by Admin only)
- `REJECTED` → `REOPENED` (REOPEN by Viewer/Manager)
- `REOPENED` → `CREATED` (SUBMIT by Viewer)

**Response (200 OK):**
```json
{
  "success": true,
  "data": {
    "id": 1,
    "title": "Process Payment Request",
    "state": "REVIEWED",
    "comments": "Ready for review",
    "updatedAt": "2026-01-10T20:10:00"
  },
  "message": "Workflow transitioned successfully"
}
```

### 7. Trigger Workflow by Name
**POST** `/api/v1/workflows/{workflowName}/trigger`

**Request:**
```json
{
  "source": "python-integration-service",
  "payload": {
    "invoiceId": "INV-2026-001",
    "amount": 5000.00,
    "vendor": "ABC Corp"
  },
  "action": "SUBMIT",
  "comments": "Automated trigger from Python service",
  "workflowId": null,
  "metadata": {}
}
```

**Response (200 OK):**
```json
{
  "success": true,
  "data": {
    "status": "SUCCESS",
    "workflowId": 2,
    "workflowName": "payment-processing",
    "state": "CREATED",
    "message": "Workflow triggered successfully",
    "correlationId": "abc123-def456-ghi789"
  }
}
```

### 8. Delete Workflow
**DELETE** `/api/v1/workflows/{id}`

**Required Role:** Admin only

**Response (200 OK):**
```json
{
  "success": true,
  "data": null,
  "message": "Workflow deleted successfully"
}
```

## Audit Log Endpoints

**Required Roles:** Reviewer, Admin, or Manager (for basic audit logs)  
**Required Roles:** Reviewer or Admin (for entity-specific audit logs)

### 1. Get Audit Logs
**GET** `/api/v1/audit?action=USER_CREATED&entityType=User&page=0&size=50`

**Query Parameters:**
- `action` (optional) - Filter by action: `USER_CREATED`, `WORKFLOW_UPDATED`, etc.
- `entityType` (optional) - Filter by entity type: `User`, `Workflow`
- `entityId` (optional) - Filter by entity ID
- `userId` (optional) - Filter by user ID who performed the action
- `fromDate` (optional) - Start date (ISO 8601 format)
- `toDate` (optional) - End date (ISO 8601 format)
- `correlationId` (optional) - Filter by correlation ID
- `page` (optional, default: 0)
- `size` (optional, default: 50)
- `sort` (optional, default: createdAt)

**Response (200 OK):**
```json
{
  "success": true,
  "data": {
    "content": [
      {
        "id": 1,
        "action": "USER_CREATED",
        "entityType": "User",
        "entityId": 2,
        "details": "User created: john_doe",
        "performedBy": {
          "id": 1,
          "username": "admin"
        },
        "ipAddress": "192.168.1.100",
        "correlationId": "abc123-def456",
        "createdAt": "2026-01-10T20:00:00"
      }
    ],
    "totalElements": 1,
    "totalPages": 1
  }
}
```

### 2. Get Audit Logs by Entity
**GET** `/api/v1/audit/entity/{entityType}/{entityId}?page=0&size=50`

**Example:** `/api/v1/audit/entity/Workflow/1`

## Integration Endpoints

### 1. Trigger Workflow (Integration)
**POST** `/api/v1/integration/workflows/trigger`

**Request:**
```json
{
  "source": "ai-ml-service",
  "payload": {
    "workflowType": "risk-assessment",
    "data": {
      "transactionId": "TXN-123",
      "amount": 50000.00
    }
  },
  "action": "SUBMIT",
  "comments": "AI-generated workflow trigger"
}
```

### 2. Integration Health Check
**GET** `/api/v1/integration/health`

**Response (200 OK):**
```json
{
  "success": true,
  "data": {
    "status": "UP",
    "service": "IEODP Integration API",
    "version": "v1",
    "timestamp": "2024-01-15T10:30:00"
  }
}
```

## Error Responses

### 401 Unauthorized
```json
{
  "success": false,
  "message": "Unauthorized",
  "errorCode": "UNAUTHORIZED",
  "timestamp": "2026-01-10T20:00:00"
}
```

### 403 Forbidden
```json
{
  "success": false,
  "message": "Access denied. Insufficient permissions.",
  "errorCode": "FORBIDDEN",
  "timestamp": "2026-01-10T20:00:00"
}
```

### 404 Not Found
```json
{
  "success": false,
  "message": "Resource not found",
  "errorCode": "NOT_FOUND",
  "timestamp": "2026-01-10T20:00:00"
}
```

### 400 Bad Request
```json
{
  "success": false,
  "message": "Validation failed",
  "errorCode": "VALIDATION_ERROR",
  "timestamp": "2026-01-10T20:00:00"
}
```

## Role-Based Access Summary

| Endpoint | Viewer | Manager | Reviewer | Admin |
|----------|--------|---------|----------|-------|
| Register/Login | ✅ | ✅ | ✅ | ✅ |
| Get User by ID | ✅ | ✅ | ✅ | ✅ |
| Get All Users | ❌ | ✅ | ❌ | ✅ |
| Search Users | ❌ | ✅ | ❌ | ✅ |
| Update User | ❌ | ✅ | ❌ | ✅ |
| Delete User | ❌ | ❌ | ❌ | ✅ |
| Create Workflow | ✅ | ✅ | ❌ | ✅ |
| Get Workflows | ✅ | ✅ | ✅ | ✅ |
| Update Workflow | ✅ | ✅ | ❌ | ✅ |
| Transition Workflow | ✅* | ✅ | ❌ | ✅ |
| Delete Workflow | ❌ | ❌ | ❌ | ✅ |
| Get Audit Logs | ❌ | ✅ | ✅ | ✅ |
| Get Audit by Entity | ❌ | ❌ | ✅ | ✅ |

*Viewer can only SUBMIT workflows (CREATED → REVIEWED, REOPENED → CREATED)

## Notes

- All timestamps are in ISO 8601 format: `YYYY-MM-DDTHH:mm:ss`
- Pagination uses Spring Data Pageable (0-indexed pages)
- All endpoints return standardized `ApiResponse<T>` wrapper
- JWT tokens expire after 1 hour (3600 seconds)
- Refresh tokens expire after 7 days
- Use correlation IDs for request tracing
- For detailed examples, see `Testing APIs.md`


## Testing

### Test Coverage Strategy

The project follows a comprehensive testing strategy:

- **Unit Tests**: Service layer and business logic (target: 80%+ coverage)
- **Repository Tests**: Data access layer with test containers
- **Controller Tests**: API endpoints with MockMvc
- **Integration Tests**: End-to-end workflows with embedded database

### Running Tests

```bash
# Run all tests
mvn test

# Run tests with coverage report
mvn test jacoco:report

# Run specific test class
mvn test -Dtest=WorkflowServiceTest

# Run tests in integration profile
mvn test -Pintegration
```

### Testing Resources

- **Postman Collection**: Import `IEODP_API_Collection.postman_collection.json`
- **API Testing Guide**: See [Testing APIs.md](Testing%20APIs.md) for detailed examples
- **Swagger UI**: Interactive API testing at http://localhost:8080/swagger-ui.html

## Database Indexing Strategy

Indexes are defined on:
- User: `username`, `email`
- WorkflowItem: `state`, `created_by_id`, `assigned_to_id`, `created_at`
- AuditLog: `action`, `performed_by_id`, `entity_type/entity_id`, `created_at`, `correlation_id`
- RefreshToken: `token`, `user_id`, `expiry_date`

## Production Deployment

### Pre-Deployment Checklist

#### Security
- [ ] Change JWT secret key (use strong, randomly generated secret)
- [ ] Change default admin password
- [ ] Enable HTTPS/TLS encryption
- [ ] Configure CORS properly (restrict allowed origins)
- [ ] Review and update security configuration
- [ ] Enable rate limiting (consider Spring Cloud Gateway or similar)
- [ ] Set up security headers (HSTS, CSP, etc.)

#### Database
- [ ] Configure connection pooling (HikariCP settings optimized)
- [ ] Set up automated database backups
- [ ] Configure database replication (if needed)
- [ ] Monitor query performance and optimize slow queries
- [ ] Set up database connection monitoring
- [ ] Configure transaction timeout settings

#### Configuration
- [ ] Update `application-prod.yaml` with production values
- [ ] Configure externalized configuration (Config Server, environment variables)
- [ ] Set appropriate log levels (INFO for production)
- [ ] Configure logging output (files, centralized logging)
- [ ] Set up environment-specific profiles

#### Monitoring & Logging
- [ ] Configure log aggregation (ELK Stack, Splunk, CloudWatch, etc.)
- [ ] Set up application monitoring (Prometheus, New Relic, Datadog)
- [ ] Configure health checks (`/actuator/health`)
- [ ] Set up alerting for critical errors
- [ ] Monitor correlation IDs for request tracing
- [ ] Configure log retention policies

#### Performance
- [ ] Enable JPA query caching where appropriate
- [ ] Monitor and optimize N+1 query issues
- [ ] Review and optimize database indexes
- [ ] Configure connection pool size based on load
- [ ] Set up CDN for static resources (if applicable)
- [ ] Consider implementing Redis for session/cache (future enhancement)

#### High Availability
- [ ] Set up load balancing (multiple application instances)
- [ ] Configure database failover/replication
- [ ] Set up health checks for load balancer
- [ ] Implement circuit breakers for external services
- [ ] Configure graceful shutdown

### Environment Variables

Key environment variables for production:

```bash
# Database
SPRING_DATASOURCE_URL=jdbc:mysql://prod-db:3306/ieodp_db
SPRING_DATASOURCE_USERNAME=prod_user
SPRING_DATASOURCE_PASSWORD=<secure_password>

# JWT
JWT_SECRET=<strong_random_secret>
JWT_EXPIRATION=3600
JWT_REFRESH_EXPIRATION=604800

# Python Service
PYTHON_SERVICE_BASE_URL=http://python-service:8000
PYTHON_SERVICE_CONNECT_TIMEOUT=5000
PYTHON_SERVICE_READ_TIMEOUT=10000

# Logging
LOGGING_LEVEL=INFO
LOGGING_FILE_PATH=/var/log/ieodp/application.log
```

### Docker Deployment (Optional)

```bash
# Build Docker image
docker build -t ieodp:latest .

# Run container
docker run -d \
  -p 8080:8080 \
  -e SPRING_DATASOURCE_URL=jdbc:mysql://db:3306/ieodp_db \
  -e JWT_SECRET=<secret> \
  --name ieodp \
  ieodp:latest
```

## Integration & Extensibility

### Integration Points

The platform is designed for seamless integration with various systems:

**Frontend Applications:**
- React, Angular, Vue.js applications
- RESTful API with JWT authentication
- CORS configured for cross-origin requests
- Standardized JSON response format

**Python/AI Services:**
- Direct integration with Python FastAPI services
- Anomaly detection, risk evaluation, decision support
- Data ingestion endpoints
- Health check monitoring
- See [Python Integration.md](Python%20Integration.md) for detailed documentation

**Analytics & BI Tools:**
- Power BI, Tableau integration via REST API
- Export endpoints for data extraction
- Real-time data access

**Microservices:**
- Versioned APIs (`/api/v1/`)
- Service-to-service authentication
- Integration health checks
- Workflow triggering from external systems

### Backward Compatibility

The platform ensures backward compatibility through:

- **API Versioning**: All endpoints use `/api/v1/` prefix
- **Version Strategy**: New versions can be added as `/api/v2/` without breaking existing clients
- **DTO Evolution**: DTOs are versioned and backward compatible
- **Deprecation Policy**: Old versions supported for at least 1 year
- **Extension Fields**: `metadata` maps in DTOs allow future additions without breaking changes

### API Documentation

- **Swagger UI**: http://localhost:8080/swagger-ui.html (interactive documentation)
- **OpenAPI JSON**: http://localhost:8080/v3/api-docs (machine-readable specification)
- **API Reference**: See [Java Backend APIs.md](Java%20Backend%20APIs.md)
- **Testing Guide**: See [Testing APIs.md](Testing%20APIs.md)

## Documentation

Comprehensive documentation is available in the following files:

- **[README.md](README.md)** - This file - Project overview and getting started
- **[Architecture.md](Architecture.md)** - System architecture, design patterns, and technical details
- **[Java Backend APIs.md](Java%20Backend%20APIs.md)** - Complete API reference with request/response examples
- **[Testing APIs.md](Testing%20APIs.md)** - Testing guide, authentication setup, and examples
- **[Python Integration.md](Python%20Integration.md)** - Python service integration documentation

## Contributing

This is a proprietary project. For contribution guidelines, please contact the project maintainers.

## License

Proprietary - All rights reserved

## Support

For issues, questions, or support requests:

- **Email**: support@ieodp.com
- **Issues**: Contact project maintainers
- **Documentation**: See documentation files listed above
- **API Documentation**: http://localhost:8080/swagger-ui.html (when running)

## Acknowledgments

Built with:
- [Spring Boot](https://spring.io/projects/spring-boot)
- [Spring Security](https://spring.io/projects/spring-security)
- [Spring Data JPA](https://spring.io/projects/spring-data-jpa)
- [OpenAPI/Swagger](https://swagger.io/)
- [Lombok](https://projectlombok.org/)

---

**Version**: 1.0.0  
**Last Updated**: 2026  
**Maintainer**: IEODP Development Java Backend Team

