<<<<<<< HEAD
# Banking System

A production-style banking system backend built with Spring Boot and SQLite, featuring JWT authentication, account management, and secure fund transfers.

![Architecture Diagram](banking.png)

## Features

- **User Authentication**: JWT-based authentication with BCrypt password hashing
- **Account Management**: Create and manage multiple bank accounts (Savings, Checking, Business)
- **Transactions**: Deposit, withdraw, and transfer funds between accounts
- **Transaction History**: View paginated transaction history for any account
- **Transactional Safety**: SERIALIZABLE isolation for transfers to ensure data consistency

## Technology Stack

- **Backend**: Java 17+, Spring Boot 3.2.x
- **Database**: SQLite (local file-based)
- **Security**: Spring Security, JWT (jjwt)
- **Build Tool**: Maven

## Prerequisites

- Java 17 or higher
- Maven 3.6+

## Getting Started

### 1. Clone and Navigate

```bash
cd banking-system
```

### 2. Build the Project

```bash
mvn clean package
```

### 3. Run the Application

```bash
mvn spring-boot:run
```

The server will start at `http://localhost:8080`.

### 4. Database

The SQLite database file (`banking.db`) will be automatically created in the project root directory when the application starts.

## Configuration

### JWT Secret (Important!)

Before deploying to production, update the JWT secret in `src/main/resources/application.properties`:

```properties
app.jwt.secret=YOUR_SECURE_256_BIT_SECRET_HERE
```

Generate a secure secret using:
```bash
openssl rand -base64 32
```

### Application Properties

Key configurations in `application.properties`:

| Property | Description | Default |
|----------|-------------|---------|
| `server.port` | Server port | 8080 |
| `app.jwt.secret` | JWT signing secret | (placeholder) |
| `app.jwt.expiration-ms` | Token expiration (ms) | 86400000 (24h) |

## API Endpoints

### Authentication

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register a new user |
| POST | `/api/auth/login` | Login and get JWT token |

### Accounts

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/accounts` | Create a new account |
| GET | `/api/accounts` | Get all accounts for current user |
| GET | `/api/accounts/{accountNumber}` | Get account details |

### Transactions

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/transactions/deposit` | Deposit funds |
| POST | `/api/transactions/withdraw` | Withdraw funds |
| POST | `/api/transactions/transfer` | Transfer between accounts |
| GET | `/api/transactions/history/{accountNumber}` | Get transaction history |

## Example API Usage

### Register a User

```bash
curl -X POST http://localhost:8080/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "securepass123"
  }'
```

### Login

```bash
curl -X POST http://localhost:8080/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@example.com",
    "password": "securepass123"
  }'
```

### Create an Account

```bash
curl -X POST http://localhost:8080/api/accounts \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -d '{
    "accountType": "CHECKING"
  }'
```

### Deposit Funds

```bash
curl -X POST http://localhost:8080/api/transactions/deposit \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -d '{
    "accountNumber": "ACC-XXXXXXXXXX",
    "amount": 1000.00,
    "description": "Initial deposit"
  }'
```

### Transfer Funds

```bash
curl -X POST http://localhost:8080/api/transactions/transfer \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -d '{
    "fromAccountNumber": "ACC-XXXXXXXXXX",
    "toAccountNumber": "ACC-YYYYYYYYYY",
    "amount": 250.00,
    "description": "Payment"
  }'
```

## Running Tests

```bash
mvn test
```

## Project Structure

```
src/
├── main/
│   ├── java/com/lalit/bank/
│   │   ├── config/          # Configuration classes
│   │   ├── controller/      # REST controllers
│   │   ├── dto/             # Data transfer objects
│   │   ├── entity/          # JPA entities
│   │   ├── exception/       # Custom exceptions
│   │   ├── repository/      # JPA repositories
│   │   ├── security/        # JWT and security
│   │   └── service/         # Business logic
│   └── resources/
│       └── application.properties
└── test/
    └── java/com/lalit/bank/
        └── TransactionIntegrationTest.java
```

## Frontend

A React-based frontend is available in the `web-ui/` directory. See `web-ui/README.md` for setup instructions.

## SQLite Limitations

SQLite is suitable for development and small-scale deployments. For production environments with high concurrency, consider migrating to PostgreSQL or MySQL. The application uses SERIALIZABLE transaction isolation to ensure data consistency despite SQLite's limited row-level locking support.

## License

MIT License
=======
# Secure Digital Banking Application on Microsoft Azure

> Enterprise-grade deployment of a two-tier digital banking application on Microsoft Azure using Azure App Service, Azure SQL Database, Private Networking, Azure Key Vault, Managed Identity and Azure DevOps CI/CD.

<p align="center">

![Azure](https://img.shields.io/badge/Microsoft%20Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Azure DevOps](https://img.shields.io/badge/Azure%20DevOps-0078D4?style=for-the-badge&logo=azuredevops&logoColor=white)
![Java](https://img.shields.io/badge/Java%2021-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Azure SQL](https://img.shields.io/badge/Azure%20SQL-0078D4?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)
![Key Vault](https://img.shields.io/badge/Azure%20Key%20Vault-005BA1?style=for-the-badge&logo=microsoftazure&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</p>

---

# Table of Contents

- [Project Overview](#project-overview)
- [Business Objective](#business-objective)
- [Solution Architecture](#solution-architecture)
- [Technology Stack](#technology-stack)
- [Azure Resources](#azure-resources)
- [Architecture Highlights](#architecture-highlights)
- [Project Features](#project-features)
- [CI/CD Workflow](#cicd-workflow)
- [Application Flow](#application-flow)
- [Security Controls](#security-controls)
- [Repository Structure](#repository-structure)
- [Deployment Roadmap](#deployment-roadmap)
- [Validation Checklist](#validation-checklist)
- [Future Enhancements](#future-enhancements)
- [Acknowledgements](#acknowledgements)

---

# Project Overview

This project demonstrates the deployment of a **secure enterprise-grade two-tier digital banking application** on **Microsoft Azure** using modern cloud architecture, secure networking practices, and an automated Azure DevOps CI/CD pipeline.

The application consists of:

- React Frontend
- Spring Boot Backend
- Azure SQL Database
- Azure App Service (Linux)
- Azure Key Vault
- Azure Virtual Network
- Azure DevOps YAML Pipeline

The solution emphasizes **security-first architecture**, ensuring that all application components communicate through private networking while eliminating unnecessary public exposure.

---

# Business Objective

Design, deploy and automate a secure banking application that demonstrates enterprise cloud architecture and DevOps practices by:

- Deploying the application on Azure App Service
- Hosting the database in Azure SQL Database
- Eliminating public database access
- Securing secrets using Azure Key Vault
- Using Managed Identity for authentication
- Restricting communication using Private Endpoints
- Automating deployment using Azure DevOps YAML Pipelines
- Implementing least-privilege network security

---

# Solution Architecture

> **Architecture Diagram**

<p align="center">


<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/1f56bc78-31da-460f-b9f8-485b7fdeac66" />


</p>

---

# Technology Stack

| Category | Technology |
|------------|------------|
| Cloud Platform | Microsoft Azure |
| CI/CD | Azure DevOps |
| Source Control | GitHub |
| Backend | Spring Boot |
| Frontend | React |
| Runtime | Java 21 |
| Database | Azure SQL Database |
| Secret Management | Azure Key Vault |
| Identity | Managed Identity |
| Networking | Azure Virtual Network |
| Security | NSG, Private Endpoint, Private DNS |
| Build Tool | Maven |
| Frontend Build | Node.js, npm |
| Operating Systems | Ubuntu Linux, Windows Server |

---

# Azure Resources

| Azure Resource | Purpose |
|----------------|---------|
| Resource Group | Logical container for Azure resources |
| Virtual Network | Private communication between resources |
| Windows Web VM | Application testing |
| Windows Database VM | SQL administration |
| Ubuntu VM | Azure DevOps Self-hosted Agent |
| Azure App Service (Linux) | Hosts banking application |
| Azure SQL Database | Banking data |
| Azure Key Vault | Secure storage for secrets |
| Private Endpoints | Private connectivity |
| Private DNS Zones | Internal name resolution |
| Network Security Groups | Network traffic filtering |

---

# Architecture Highlights

### Azure DevOps

- YAML Pipeline
- Azure Resource Manager Service Connection
- Self-hosted Ubuntu Agent

### Compute

- Azure App Service (Linux)
- Windows Web VM
- Windows Database VM
- Ubuntu DevOps Agent

### Networking

- Azure Virtual Network
- Web Subnet
- Database Subnet
- Agent Subnet
- Integration Subnet
- Private Endpoint Subnet

### Security

- Private Endpoints
- Private DNS
- Network Security Groups
- Managed Identity
- Azure Key Vault RBAC

### Database

- Azure SQL Database
- Public Network Access Disabled

---

# Project Features

- Azure App Service (Linux)
- Azure SQL Database
- Azure Key Vault
- Azure Virtual Network
- Private Endpoints
- Private DNS
- Azure DevOps YAML Pipeline
- Self-hosted Azure DevOps Agent
- Managed Identity Authentication
- Role-Based Access Control (RBAC)
- Network Security Groups
- Spring Boot Deployment
- React Build Integration
- Automated CI/CD
- Secure Secret Management
- Enterprise Network Segmentation

---

# CI/CD Workflow

```
Developer
      │
      ▼
GitHub Repository
      │
      ▼
Azure DevOps Pipeline
      │
      ▼
Self-hosted Ubuntu Agent
      │
      ▼
Install Dependencies
      │
      ▼
Build React Frontend
      │
      ▼
Build Spring Boot Backend
      │
      ▼
Run Tests
      │
      ▼
Package Application (JAR)
      │
      ▼
Deploy to Azure App Service
      │
      ▼
Application Running
```

---

# Application Flow

```
User
      │
      ▼
Windows Web VM
      │
      ▼
Azure App Service
      │
      ▼
Managed Identity
      │
      ▼
Azure Key Vault
      │
      ▼
Azure SQL Database
```

---

# Security Controls

| Security Feature | Status |
|------------------|--------|
| Azure SQL Public Access Disabled | ✅ |
| Azure Key Vault Public Access Disabled | ✅ |
| Private Endpoints | ✅ |
| Private DNS | ✅ |
| Managed Identity | ✅ |
| RBAC | ✅ |
| Network Security Groups | ✅ |
| Azure DevOps Self-hosted Agent | ✅ |
| Least Privilege Access | ✅ |
| Secure Secret Management | ✅ |

---

# Repository Structure

```
Secure-Digital-Banking-Azure
│
├── README.md
├── LICENSE
├── azure-pipelines.yml
│
├── docs
│   ├── Architecture
│   │      ├── Solution-Architecture.png
│   │      ├── Network-Topology.png
│   │      ├── Application-Flow.png
│   │      └── CI-CD-Flow.png
│   │
│   ├── Architecture.md
│   ├── Deployment-Guide.md
│   ├── Networking.md
│   ├── Security.md
│   ├── Pipeline.md
│   └── Screenshots
│
├── application
│
└── scripts
```

---

# Deployment Roadmap

1. Create Azure Resource Group
2. Create Virtual Network
3. Create Subnets
4. Configure Network Security Groups
5. Deploy Windows Web VM
6. Deploy Windows Database VM
7. Deploy Ubuntu Self-hosted Agent
8. Deploy Azure SQL Database
9. Configure Private Endpoint
10. Configure Private DNS
11. Deploy Azure Key Vault
12. Configure Managed Identity
13. Deploy Azure App Service
14. Configure Azure DevOps
15. Create YAML Pipeline
16. Deploy Banking Application
17. Validate Secure Connectivity

---

# Validation Checklist

| Validation | Expected Result |
|------------|-----------------|
| Web VM accesses Application | ✅ |
| Database VM accesses Azure SQL | ✅ |
| App Service accesses Azure SQL | ✅ |
| App Service retrieves Key Vault Secrets | ✅ |
| Azure SQL Public Access Disabled | ✅ |
| Key Vault Public Access Disabled | ✅ |
| Private Endpoint Connectivity | ✅ |
| Azure DevOps Pipeline Success | ✅ |
| Application Deployment Successful | ✅ |

---

# Future Enhancements

- Azure Front Door
- Azure Application Gateway
- Web Application Firewall (WAF)
- Azure Monitor
- Application Insights
- Log Analytics Workspace
- Azure Container Apps
- Azure Kubernetes Service (AKS)
- Blue-Green Deployment
- Canary Deployment
- Infrastructure as Code (Terraform/Bicep)
- SonarQube Integration
- GitHub Actions Pipeline
- Automated Security Scanning

---

# Acknowledgements

This project is built as a practical demonstration of enterprise Azure Cloud and Azure DevOps implementation using a publicly available banking application as the application layer.

The focus of this repository is the design and implementation of secure cloud infrastructure, networking, identity management, and automated CI/CD deployment on Microsoft Azure.

---

## Author

**Pratyusha Gatta**

Azure Cloud | DevOps | CI/CD | Cloud Security | Infrastructure Automation

LinkedIn: *(Add your profile)*

GitHub: *(Add your GitHub profile)*

---

> **Note:** This project is intended for educational and portfolio purposes to demonstrate enterprise cloud architecture, Azure networking, DevOps automation, and secure application deployment using Microsoft Azure services.
>>>>>>> e6e38f226597dcc01b79a9d131b369ebefbc319f
