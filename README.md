# TaskTrackerApp - Spring Boot Application

A comprehensive Spring Boot application demonstrating various Spring concepts including bean scopes, annotations, qualifiers, and dependency injection.

## 🚀 Features Implemented

### 1. **Bean Scopes**
- **Singleton** (default): `SmsNotificationService` - Same instance for all injections
- **Prototype**: `EmailNotificationService` - New instance for each injection
- **Request**: `requestScopedNotificationService` - New instance per HTTP request

### 2. **Dependency Injection Types**
- **Constructor Injection** (Preferred): Used in all service classes and controllers
- **Field Injection**: Demonstrated with `@Autowired` in Main class
- **Setter Injection**: Available but not used (constructor injection preferred)

### 3. **Annotations Used**
- `@SpringBootApplication` - Main application class
- `@Service` - Service layer components
- `@Repository` - Data access layer
- `@RestController` - REST API controllers
- `@Component` - General Spring components
- `@Configuration` - Configuration classes
- `@Bean` - Bean definitions
- `@Scope` - Bean scope definitions
- `@Qualifier` - Bean qualification for multiple implementations
- `@Autowired` - Dependency injection
- `@Transactional` - Transaction management
- `@Entity` - JPA entities
- `@Table`, `@Column`, `@Id`, `@GeneratedValue` - JPA annotations

### 4. **Qualifiers**
- `@Qualifier("emailNotificationService")` - For email notifications
- `@Qualifier("smsNotificationService")` - For SMS notifications
- Multiple implementations of `NotificationService` interface

### 5. **HTTP APIs Available**

#### Task APIs
- `GET /api/tasks` - Get all tasks
- `POST /api/tasks` - Create new task
- `GET /api/tasks/{id}` - Get task by ID
- `PUT /api/tasks/{id}` - Update task
- `PATCH /api/tasks/{id}/status` - Update task status
- `DELETE /api/tasks/{id}` - Delete task
- `GET /api/tasks/user/{userId}` - Get tasks by user
- `GET /api/tasks/status/{status}` - Get tasks by status
- `GET /api/tasks/search?title=keyword` - Search tasks by title
- `GET /api/tasks/stats/status/{status}` - Get task count by status

#### User APIs
- `GET /api/users` - Get all users
- `POST /api/users` - Create new user
- `GET /api/users/{id}` - Get user by ID
- `GET /api/users/username/{username}` - Get user by username
- `PUT /api/users/{id}` - Update user
- `DELETE /api/users/{id}` - Delete user
- `GET /api/users/with-tasks` - Get all users with their tasks
- `GET /api/users/search?fullName=name` - Search users by full name
- `POST /api/users/{userId}/tasks` - Add task to user

## 🏗️ Architecture

### Model Layer
- `Task` - Task entity with JPA annotations
- `User` - User entity with JPA annotations
- `TaskStatus` - Enum for task statuses
- `TaskPriority` - Enum for task priorities

### Repository Layer
- `TaskRepository` - JPA repository for Task operations
- `UserRepository` - JPA repository for User operations

### Service Layer
- `TaskService` - Business logic for tasks (uses EmailNotificationService)
- `UserService` - Business logic for users (uses SmsNotificationService)
- `NotificationService` - Interface for notifications
- `EmailNotificationService` - Email notification implementation
- `SmsNotificationService` - SMS notification implementation

### Controller Layer
- `TaskController` - REST endpoints for task operations
- `UserController` - REST endpoints for user operations

### Configuration Layer
- `AppConfig` - Bean definitions and configurations
- `DatabaseConfig` - JPA and database configuration
- `WebConfig` - Web configuration (CORS, etc.)

## 🛠️ Technologies Used

- **Spring Boot 3.2.0**
- **Spring Data JPA**
- **H2 Database** (In-Memory)
- **Maven** for dependency management
- **Java 17**

## 🚀 How to Run

1. **Prerequisites**
   - Java 17 or higher
   - Maven 3.6+

2. **Run the Application**
   ```bash
   mvn spring-boot:run
   ```

3. **Access the Application**
   - Application: http://localhost:8080
   - H2 Console: http://localhost:8080/h2-console
     - JDBC URL: `jdbc:h2:mem:tasktracker`
     - Username: `sa`
     - Password: (leave empty)

## 📝 Sample API Usage

### Create a User
```bash
curl -X POST http://localhost:8080/api/users \
  -H "Content-Type: application/json" \
  -d '{
    "username": "test_user",
    "email": "test@example.com",
    "fullName": "Test User"
  }'
```

### Create a Task
```bash
curl -X POST http://localhost:8080/api/tasks \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Learn Spring Boot",
    "description": "Complete Spring Boot tutorial",
    "priority": "HIGH",
    "status": "PENDING",
    "user": {
      "id": 1
    }
  }'
```

### Get All Tasks
```bash
curl http://localhost:8080/api/tasks
```

## 🔧 Key Spring Concepts Demonstrated

1. **Constructor Injection** - Preferred method used throughout
2. **Bean Scopes** - Singleton, Prototype, Request scopes
3. **Qualifiers** - Multiple implementations of same interface
4. **Annotations** - Comprehensive use of Spring annotations
5. **Configuration** - Java-based configuration classes
6. **Transaction Management** - `@Transactional` annotations
7. **REST APIs** - Complete CRUD operations
8. **Database Integration** - JPA with H2 database

## 📊 Database Schema

The application uses JPA entities with the following relationships:
- **User** (1) → (Many) **Task**
- Tasks belong to users
- Automatic timestamp management
- Enum support for status and priority

This implementation demonstrates best practices in Spring Boot development with proper separation of concerns, dependency injection, and comprehensive API design.
