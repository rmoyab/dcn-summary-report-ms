# Summary Report Service

A Spring Boot microservice for generating, storing, and retrieving summary reports of patient vital signs. Reports are saved as JSON files in AWS S3 and metadata is stored in an Oracle database.

## Features

- Consumes vital signs data from RabbitMQ (`summaryQueue`)
- Generates summary reports in JSON format
- Uploads reports to AWS S3
- Stores report metadata in Oracle DB
- REST API to list and download reports

## Stack

- Java 23
- Maven
- Docker
- Oracle Database (with wallet for secure connection)
- AWS S3 bucket
- RabbitMQ

## API Endpoints

- `GET /api/reports` List all summary reports.

- `GET /api/reports/{id}` Download a specific report by its ID.

## Project Structure

```text
src/
├── config
│   └── RabbitMQConfig.java
├── controller
│   └── SummaryReportController.java
├── init
│   └── DataInitializer.java
├── model
│   ├── SummaryReport.java
│   └── VitalSigns.java
├── repository
│   └── SummaryReportRepository.java
├── service
│   ├── S3Service.java
│   ├── SummaryReportConsumer.java
│   ├── SummaryReportService.java
│   └── SummaryReportServiceImpl.java
├── utils
│   └── Utils.java
└── App.java
```

## Best Practices

- **Layered Architecture:** Clear separation of concerns between controller, service, repository, and configuration layers.
- **Dependency Injection:** Uses Spring's `@Autowired` and constructor injection for loose coupling and easier testing.
- **Configuration Management:** Sensitive data and environment-specific settings are externalized using `application.yml` and environment variables.
- **Exception Handling:** Centralized exception handling for REST endpoints (using `@ControllerAdvice` if implemented).
- **Logging:** Uses SLF4J for consistent and configurable logging.
- **DTOs and Models:** Distinct model classes for data transfer and persistence.
- **Unit and Integration Testing:** Testable service and repository layers (see `/test` directory).
- **Externalized Secrets:** Database credentials and AWS keys are not hardcoded.
- **Containerization:** Docker support for consistent deployment environments.
- **Code Quality:** Follows Java naming conventions and code organization for readability and maintainability.
- **Documentation:** Well-documented code and API endpoints.
