Project Description: This is a Patient Management Microservices System built with Spring Boot, showcasing modern cloud-native architecture patterns.

Core Purpose: A distributed system for managing patient registrations, billing, and analytics using a microservices architecture with inter-service communication via gRPC and Kafka event streaming.

Key Microservices

1. Patient Service (Port 4000) - Core patient CRUD operations with PostgreSQL persistence. Triggers billing account creation and publishes events when patients are registered.

2. Billing Service (Port 9001 gRPC) - Stateless service that creates billing accounts for new patients via gRPC calls from Patient Service.

3. Analytics Service (Port 4002) - Event-driven service that consumes and processes patient events from Kafka asynchronously.

4. Auth Service (Port 4005) - JWT-based authentication with PostgreSQL user storage. Issues tokens with 10-hour expiration and validates requests.

5. API Gateway (Port 4004) - Spring Cloud Gateway acting as single entry point, routes requests to backend services and enforces JWT validation on protected endpoints.

Architecture Highlights

1. Synchronous Communication: gRPC between Patient and Billing services
2. Asynchronous Communication: Kafka event streaming for analytics processing
3. Security: JWT-based authentication with centralized Auth Service
4. Data Persistence: PostgreSQL for Patient and Auth services
5. Containerization: Docker with multi-stage builds for each service
6. Infrastructure: AWS CDK defines ECS Fargate cluster, RDS databases, and MSK Kafka

Technology Stack: Java 17/21, Spring Boot 4.1.0, gRPC, Kafka, PostgreSQL, JWT, Docker, AWS (ECS, RDS, MSK, CDK)

Data Flow: When a patient is created: REST API → API Gateway (validates JWT) → Patient Service (saves to DB, calls Billing Service via gRPC, publishes Kafka event) → Analytics Service (consumes event asynchronously)
