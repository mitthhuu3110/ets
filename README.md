# Employee Tracking System (ETS)

The Employee Tracking System (ETS) is a RESTful web application built with Spring Boot, Spring Data JPA, and PostgreSQL. It allows organizations to manage employee records efficiently, supporting CRUD operations and scalable deployment.

---

## Table of Contents

- [Features](#features)
- [Architecture](#architecture)
- [Technology Stack](#technology-stack)
- [Database Schema](#database-schema)
- [API Endpoints](#api-endpoints)
- [Getting Started](#getting-started)
- [Build & Run](#build--run)
- [Testing](#testing)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)

---

## Features

- Add, update, view, and delete employee records
- RESTful API design
- PostgreSQL database integration
- Dockerized for easy deployment
- Secure and scalable architecture

---

## Architecture

### High-Level Architecture

- **Controller Layer**: Handles HTTP requests and responses ([`com.example.employeemanagement.controller.EmployeeController`](src/main/java/com/example/employeemanagement/controller/EmployeeController.java))
- **Service Layer**: Business logic ([`com.example.employeemanagement.service.EmployeeService`](src/main/java/com/example/employeemanagement/service/EmployeeService.java))
- **Repository Layer**: Data access using Spring Data JPA ([`com.example.employeemanagement.repository.EmployeeRepository`](src/main/java/com/example/employeemanagement/repository/EmployeeRepository.java))
- **Model Layer**: Entity definitions ([`com.example.employeemanagement.model.Employee`](src/main/java/com/example/employeemanagement/model/Employee.java))

### Recommended Deployment Plan

- **Backend**: Spring Boot application running in a Docker container
- **Database**: PostgreSQL running in a separate Docker container or managed service
- **CI/CD**: Jenkins pipeline for build, test, Docker image creation, and deployment ([Jenkinsfile](Jenkinsfile))
- **Reverse Proxy (optional)**: Nginx or similar for SSL termination and routing

---

## Technology Stack

- Java 17+
- Spring Boot
- Spring Data JPA
- PostgreSQL
- Docker
- Jenkins (for CI/CD)
- Maven

---

## Database Schema

### PostgreSQL Table: `employees`

| Column      | Type         | Constraints           | Description           |
|-------------|--------------|----------------------|-----------------------|
| id          | BIGSERIAL    | PRIMARY KEY          | Employee ID           |
| name        | VARCHAR(255) | NOT NULL             | Employee Name         |
| email       | VARCHAR(255) | NOT NULL, UNIQUE     | Employee Email        |
| department  | VARCHAR(255) | NOT NULL             | Department Name       |

#### SQL DDL

```sql
CREATE TABLE employees (
    id BIGSERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    department VARCHAR(255) NOT NULL
);
```