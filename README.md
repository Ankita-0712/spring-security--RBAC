# spring-security--RBAC

A Spring Boot application implementing JWT-based authentication and Role-Based Access Control (RBAC). This project demonstrates a secure and scalable backend design, where users are authenticated using JSON Web Tokens (JWTs) and authorized to access specific resources based on their roles.

# Overview

The SecurityDemo application is a secure backend API server where:

- Users can authenticate using their credentials.
- A JWT is generated upon successful login.
- The application supports RBAC to grant or deny access to endpoints based on the user's assigned roles.

# Project Structure and File Details

1. **JwtUtils**  
   Handles all JWT-related operations:
   - Generates JWT tokens.
   - Validates tokens.
   - Extracts username and roles from the token.

2. **AuthTokenFilter**  
   A Spring Security filter that intercepts requests:
   - Parses the JWT from the `Authorization` header.
   - Validates the token using `JwtUtils`.
   - Authenticates the user and sets the security context.

3. **AuthEntryPointJwt**  
   Handles unauthorized access attempts:
   - Returns an HTTP 401 status with a custom error message.

4. **LoginRequest**  
   Represents the payload for login requests:
   - Contains username and password.

5. **LoginResponse**  
   Represents the response for successful logins:
   - Includes the JWT token, username, and user roles.

6. **SecurityConfig**  
   Configures Spring Security for the application:
   - Sets up JWT authentication filters.
   - Defines role-based access to endpoints.
   - Uses `AuthEntryPointJwt` to handle unauthorized access.

7. **GreetingsController**  
   Provides endpoints for testing RBAC.

8. **MainApplication**  
   The main entry point for the Spring Boot application.

# Architecture

### Authentication Flow

1. **Login:**  
   Users provide their username and password via the `/api/auth/login` endpoint.

2. **JWT Token Generation:**  
   A signed JWT is issued upon successful authentication, containing the user's details and roles.

3. **Token Validation:**  
   Every request to protected resources includes the JWT in the `Authorization` header. The server validates the token and extracts the user's roles.

4. **Access Control:**  
   Based on the user's roles, specific resources or endpoints are either granted or denied.

### Diagram:

```plaintext
[ Client ] ---> [ Auth API (Login) ] ---> [ JWT Generated ]
     |
     +--> [ Secured API Endpoint ] ---> [ AuthTokenFilter ]
                    |
                    +--> [ JWT Validation ] ---> [ RBAC Decision ]
```

# Features

### Secure Authentication:
- Implements JWT for stateless authentication.
- Tokens are signed using HMAC-SHA for integrity.

### Role-Based Access Control (RBAC):
- Role-specific access to API endpoints.
- Multiple roles per user supported.

### Token Validation:
- Middleware filter (`AuthTokenFilter`) for token validation and user authentication.

### Error Handling:
- Custom error responses for unauthorized or invalid requests.

# Role-Based Access Control (RBAC)

RBAC is implemented to control access based on user roles. Each role determines which endpoints a user can access.

### Example

- **Admin Role:**
  - Full access to admin-specific endpoints.

- **User Role:**
  - Access only to user-specific endpoints.

Roles are stored in the database and embedded into the JWT during login.
