
# LeaveFlow API Gateway - Copilot Instructions

## Project Overview
This is the API Gateway for LeaveFlow, an Employee Leave Management System built using microservices architecture.

## Technology Stack
- Java 21
- Spring Boot 3.5.x
- Spring Cloud Gateway (Reactive)
- Spring Security
- Spring OAuth2 Resource Server
- Maven

## Port
8080

## Architecture
The API Gateway is the single public entry point for frontend requests.

It communicates with:
- Auth Service: 8081
- Employee Service: 8082
- Leave Service: 8083
- Notification Service: 8084

## Responsibilities
1. Route requests to appropriate microservices.
2. Validate JWT access tokens.
3. Enforce authentication for protected endpoints.
4. Apply role-based authorization.
5. Configure CORS for React frontend.
6. Handle unauthorized and forbidden requests.
7. Propagate authenticated identity securely to downstream services.

## Routing
- /api/auth/** -> Auth Service
- /api/employees/** -> Employee Service
- /api/leaves/** -> Leave Service
- /api/notifications/** -> Notification Service

## Security Requirements
- Use Spring Security OAuth2 Resource Server.
- Validate JWT signature, expiration and issuer.
- Use asymmetric JWT signing: Auth Service signs tokens using a private key; Gateway verifies using the corresponding public key.
- Never expose private signing keys in this repository.
- Reject invalid or expired tokens.
- Configure public access only for authentication endpoints and health endpoints.
- Protect all other routes.
- Enforce roles: EMPLOYEE, MANAGER, ADMIN.
- Never trust identity or role headers supplied directly by clients.
- Remove spoofable identity headers before forwarding requests.
- Do not log JWT tokens or passwords.

## Coding Standards
- Use reactive WebFlux architecture.
- Use constructor injection.
- Keep gateway configuration separate.
- Use environment variables for configuration.
- Do not add Spring MVC dependencies.
- Do not implement business logic in the gateway.

## Testing
- Add tests for route configuration.
- Test valid, expired and invalid JWT scenarios.
- Test role-based authorization.
- Test CORS configuration.
- Run Maven tests after modifications.

## Important
Before modifying files:
1. Inspect existing pom.xml.
2. Check Spring Cloud compatibility.
3. Review existing security configuration.
4. Present an implementation plan.

Do not modify unrelated files.
Do not invent dependencies or arbitrary versions.
