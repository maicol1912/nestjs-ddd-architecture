# nestjs-ddd-hexagonal

<p align="center">
  <a href="http://nestjs.com/" target="_blank"><img src="https://nestjs.com/img/logo_text.svg" width="320" alt="Nest Logo" /></a>
</p>

<p align="center">
  A robust NestJS application by <strong>maicol1912</strong> demonstrating Domain-Driven Design (DDD) and Hexagonal Architecture for scalable, maintainable server-side systems.
</p>

<p align="center">
  <a href="https://www.npmjs.com/~nestjscore"><img src="https://img.shields.io/npm/v/@nestjs/core.svg" alt="NPM Version" /></a>
  <a href="https://www.npmjs.com/~nestjscore"><img src="https://img.shields.io/npm/l/@nestjs/core.svg" alt="Package License" /></a>
  <a href="https://www.npmjs.com/~nestjscore"><img src="https://img.shields.io/npm/dm/@nestjs/common.svg" alt="NPM Downloads" /></a>
  <a href="https://circleci.com/gh/nestjs/nest"><img src="https://img.shields.io/circleci/build/github/nestjs/nest/master" alt="CircleCI" /></a>
</p>

## Overview

`nestjs-ddd-hexagonal` is a personal project by **maicol1912**, built with **NestJS** to showcase the power of **Domain-Driven Design (DDD)** and **Hexagonal Architecture (Ports and Adapters)** in creating scalable, maintainable, and testable server-side applications. This project implements a sophisticated system for managing entities with secure user authentication, emphasizing clean architecture principles and best practices for enterprise-grade development.

### Key Features
- **Domain-Driven Design**: Encapsulates business logic in well-defined domain models, entities, and use cases for clarity and modularity.
- **Hexagonal Architecture**: Decouples business logic from infrastructure through ports and adapters, enabling flexibility and seamless integration with external systems.
- **Secure Authentication**: Implements JWT-based authentication with access and refresh tokens, supporting login, logout, token refresh, and user validation.
- **Database Integration**: Leverages TypeORM with PostgreSQL for robust data persistence and schema migrations.
- **API Documentation**: Provides comprehensive Swagger documentation for API endpoints, accessible in non-production environments at `/api`.
- **Robust Error Handling**: Centralized exception handling with custom filters for consistent and reliable error responses.
- **Logging**: Integrated logging system for monitoring requests, errors, and application events.
- **Testing**: Includes unit and end-to-end tests with Jest to ensure code quality and reliability.

This project serves as a reference for developers exploring advanced architectural patterns in NestJS, crafted by **maicol1912** to demonstrate technical expertise and clean design.

## Architecture

The application is structured around DDD and Hexagonal Architecture principles, ensuring a clear separation between business logic and infrastructure:

- **Domain Layer** (`src/domain`): Defines core business models, interfaces for repositories, services, and configurations, keeping business rules independent of infrastructure.
- **Use Cases Layer** (`src/usecases`): Implements business logic through use cases, orchestrating interactions between domain models and repositories.
- **Infrastructure Layer** (`src/infrastructure`): Provides adapters for external systems (e.g., TypeORM for database access, JWT for authentication) and controllers for handling HTTP requests.
- **Database** (`database`): Manages schema migrations using TypeORM to maintain a consistent database structure.

This structure promotes testability, maintainability, and scalability, making it ideal for complex, production-ready applications.

## Installation

### Prerequisites
- **Node.js**: Version specified in `.nvmrc` (LTS/Iron, Node 20).
- **Docker**: For running PostgreSQL.
- **npm**: For dependency management.

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/maicol1912/nestjs-ddd-hexagonal.git
   cd nestjs-ddd-hexagonal
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Configure environment variables:
   Create a `local.env` file in the `env` directory with the following:
   ```env
   NODE_ENV=local
   JWT_SECRET=your_jwt_secret
   JWT_EXPIRATION_TIME=1800
   JWT_REFRESH_TOKEN_SECRET=your_refresh_token_secret
   JWT_REFRESH_TOKEN_EXPIRATION_TIME=86400
   DATABASE_HOST=localhost
   DATABASE_PORT=5432
   DATABASE_USER=postgres
   DATABASE_PASSWORD=docker
   DATABASE_NAME=clean_architecture_db
   DATABASE_SCHEMA=public
   DATABASE_SYNCHRONIZE=false
   ```

4. Start PostgreSQL with Docker:
   ```bash
   docker run --name clean-architecture-db -e POSTGRES_PASSWORD=docker -p 5432:5432 -d postgres
   ```

5. Run database migrations:
   ```bash
   npm run typeorm:generate:win -n init
   npm run typeorm:run:win
   ```

## Running the Application

```bash
# Development mode
npm run start

# Watch mode (auto-reload)
npm run start:dev

# Production mode
npm run start:prod
```

The application runs on `http://localhost:3000`. In non-production environments, access Swagger API documentation at `http://localhost:3000/api`.

## API Endpoints

### Authentication
- **POST /auth/login**: Authenticates a user and issues access/refresh tokens.
- **POST /auth/logout**: Invalidates authentication tokens.
- **GET /auth/is_authenticated**: Verifies user authentication status.
- **GET /auth/refresh**: Refreshes the access token using a valid refresh token.

### Entity Management
- **GET /todo/todo?id={id}**: Retrieves an entity by ID.
- **GET /todo/todos**: Retrieves all entities.
- **POST /todo/todo**: Creates a new entity.
- **PUT /todo/todo**: Updates an entity's status.
- **DELETE /todo/todo?id={id}**: Deletes an entity by ID.

Explore the Swagger documentation (`/api`) for detailed request/response schemas and examples.

## Testing

```bash
# Run unit tests
npm run test

# Run end-to-end tests
npm run test:e2e

# Generate test coverage
npm run test:cov
```

## Project Structure

```
├── database/
│   └── migrations/          # Database migrations for schema management
├── src/
│   ├── domain/             # Core business models and interfaces
│   ├── infrastructure/     # Adapters, controllers, and services
│   ├── usecases/          # Business logic for application use cases
│   └── app.module.ts       # Root module wiring dependencies
├── test/                   # End-to-end tests
├── README.md
├── package.json
├── tsconfig.json
├── .nvmrc
└── .prettierrc
```

## About the Author

This project was created by **maicol1912** as a personal endeavor to explore and demonstrate advanced architectural patterns in NestJS. It reflects a commitment to clean code, scalability, and modern software engineering practices.
