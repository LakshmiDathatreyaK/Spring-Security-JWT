# Spring Security Example with JWT

This project is a comprehensive example of implementing **Spring Security** in a Spring Boot application using **JWT (JSON Web Token)** for stateless authentication and **MySQL** for persistent user storage.

## Features

- **User Authentication**: Secure user login and registration.
- **JWT Integration**: Stateless authentication using JSON Web Tokens.
- **Password Hashing**: Uses `BCryptPasswordEncoder` (strength 12) for secure password storage.
- **Stateless Session Management**: Configured for high scalability with `SessionCreationPolicy.STATELESS`.
- **Database Integration**: JPA/Hibernate with MySQL for user management.
- **RESTful Endpoints**: Clean API design for students and users.

## Prerequisites

- **Java**: 21 or higher
- **Maven**: 3.9+
- **MySQL**: 8.0+
- **Postman or Curl**: For testing the API

## Project Structure

- `config`: Security and JWT filter configurations.
- `controller`: REST API endpoints (`Hello`, `Student`, `User`).
- `model`: JPA entities (`Users`, `Student`) and `UserPrincipal`.
- `repo`: Spring Data JPA repositories (`UserRepo`).
- `service`: Business logic for JWT generation and user authentication.

## Setup & Installation

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd springSecurityEx
   ```

2. **Configure Database**:
   Update `src/main/resources/application.properties` with your MySQL credentials:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/your_database_name
   spring.datasource.username=your_username
   spring.datasource.password=your_password
   ```

3. **Build the project**:
   ```bash
   mvn clean install
   ```

4. **Run the application**:
   ```bash
   mvn spring-boot:run
   ```

## API Endpoints

### Public Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST   | `/register` | Register a new user |
| POST   | `/login`    | Authenticate and receive a JWT token |

### Protected Endpoints (Requires JWT)
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET    | `/` | Welcome message with Session ID |
| GET    | `/students` | Get list of all students |
| POST   | `/students` | Add a new student |
| GET    | `/csrf-token` | Get current CSRF token (if enabled) |

## Usage Guide

### 1. Register a User
Send a `POST` request to `/register`:
```json
{
    "username": "john_doe",
    "password": "password123"
}
```

### 2. Login
Send a `POST` request to `/login` with the same credentials. The response will be a **JWT Token**.

### 3. Access Protected Data
Include the JWT token in the `Authorization` header of your requests:
```text
Authorization: Bearer <your_jwt_token>
```

## Security Implementation Details
- **JWT Filter**: Intercepts every request to validate the token in the `Authorization` header.
- **Statelessness**: Since it's a REST API, CSRF is disabled and sessions are not maintained on the server.
- **Authentication Manager**: Orchestrates the authentication process using `DaoAuthenticationProvider`.

---
*Created as a learning project for Spring Security.*
