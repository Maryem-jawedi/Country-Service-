# Country Service API

A RESTful web service for managing country information, developed as part of an academic project using **Java and Spring Boot**.

The application provides CRUD (Create, Read, Update, Delete) operations to manage country records, including their names and capitals. It uses Spring Data JPA for database persistence and includes automated tests and a CI/CD pipeline.

## Authors

Academic project developed by:

- **Maryem Jawedi**
- **Lina Mansour**
- **Chayma Ben Abdallah**

## Technologies & Tools

| Category | Technologies |
|---|---|
| Programming Language | Java 17 |
| Backend Framework | Spring Boot 3.5.4 |
| Data Access | Spring Data JPA, Hibernate |
| Database | H2 Database, MySQL Connector |
| API Documentation | Swagger / OpenAPI |
| Testing | JUnit 5, Mockito, MockMvc |
| Code Coverage | JaCoCo |
| Build Management | Maven |
| Containerization | Docker |
| CI/CD | Jenkins |
| Code Quality | SonarQube |
| Artifact Repository | Nexus |

## Project Features

The Country Service API supports the following operations:

- **Retrieve all countries:** Get the complete list of countries.
- **Retrieve a country by ID:** Find a country using its unique identifier.
- **Retrieve a country by name:** Search for a country by its name.
- **Add a country:** Create a new country record.
- **Update a country:** Modify an existing country's information.
- **Delete a country:** Remove a country from the database.

Each country contains three attributes:

- `idCountry`: Unique country identifier.
- `name`: Country name.
- `capital`: Country capital.

## Project Architecture

The application follows a layered architecture to separate responsibilities and improve maintainability.

```text
src/
├── main/
│   ├── java/com/countryservice/demo/
│   │   ├── beans/
│   │   │   └── Country.java
│   │   ├── controllers/
│   │   │   └── CountryController.java
│   │   ├── repositories/
│   │   │   └── CountryRepository.java
│   │   ├── services/
│   │   │   └── CountryService.java
│   │   └── CountryServiceApplication.java
│   │
│   └── resources/
│       └── application.properties/
│
└── test/
    └── java/com/countryservice/demo/
        ├── ControllerMockMvcTests.java
        ├── ControllerMockitoTests.java
        ├── ServiceMockitoTests.java
        └── CountryServiceApplicationTests.java
```

### Main Components

- **Controller Layer:** Handles HTTP requests and defines REST API endpoints.
- **Service Layer:** Implements the business logic and country management operations.
- **Repository Layer:** Manages database interactions through Spring Data JPA.
- **Entity Layer:** Defines the Country entity and its database mapping.

## API Endpoints

The application runs by default on port `8082`.

Base URL:

```text
http://localhost:8082
```

| HTTP Method | Endpoint | Description |
|---|---|---|
| GET | `/getcountries` | Retrieve all countries |
| GET | `/getcountries/{id}` | Retrieve a country by ID |
| GET | `/getcountries/countryname?name=France` | Retrieve a country by name |
| POST | `/addcountry` | Add a new country |
| PUT | `/updatecountry/{id}` | Update an existing country |
| DELETE | `/deletecountry/{id}` | Delete a country |

### Example API Requests

**1. Add a country**

`POST /addcountry`

Request body:

```json
{
  "idCountry": 1,
  "name": "France",
  "capital": "Paris"
}
```

**2. Update a country**

`PUT /updatecountry/1`

Request body:

```json
{
  "name": "Germany",
  "capital": "Berlin"
}
```

**3. Retrieve all countries**

`GET /getcountries`

**4. Delete a country**

`DELETE /deletecountry/1`

## Getting Started

### Prerequisites

Make sure you have installed:

- Java Development Kit (JDK) 17 or later.
- Maven 3.6+ (or use the included Maven Wrapper).
- Git.

### 1. Clone the repository

```bash
git clone <YOUR_REPOSITORY_URL>
```

### 2. Navigate to the project directory

```bash
cd Country-service-main
```

### 3. Run the application

On Linux / macOS:

```bash
./mvnw spring-boot:run
```

On Windows:

```bash
mvnw.cmd spring-boot:run
```

The application will start at:

`http://localhost:8082`

### 4. Access API Documentation

Swagger UI is available at:

`http://localhost:8082/swagger-ui/index.html`

It allows you to explore and test the available REST API endpoints.

## Database Configuration

The project uses an in-memory **H2 database** by default.

Configuration:

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.h2.console.enabled=true

server.port=8082
```

The H2 console can be accessed at:

`http://localhost:8082/h2-console`

The project also includes a MySQL configuration as an alternative database setup.

**Note:** Since H2 runs in memory, database records are not persistent after the application stops.

## Testing

The project includes automated tests to validate application behavior and business logic.

Testing technologies:

- **JUnit 5:** Unit testing.
- **Mockito:** Mocking dependencies and isolating components.
- **MockMvc:** Testing REST controller endpoints.
- **JaCoCo:** Measuring code coverage and generating coverage reports.

Run the test suite:

```bash
./mvnw clean test
```

Generate the JaCoCo coverage report:

```bash
./mvnw clean test
```

The report is generated at:

```text
target/site/jacoco/index.html
```

## CI/CD Pipeline

The project includes a Jenkins pipeline (`jenkinsfile`) with three main stages:

1. **Build, Test and Package**
   - Compile the application.
   - Execute automated tests.
   - Package the application.
   - Publish test results and JaCoCo coverage reports.

2. **SonarQube Analysis**
   - Analyze source code quality.
   - Run static code analysis.

3. **Deploy to Nexus**
   - Deploy the generated Maven artifact to the configured Nexus repository.

The pipeline requires Jenkins, Maven, SonarQube and Nexus to be configured in the execution environment.

## Docker Support

A Dockerfile is provided to containerize the Spring Boot application.

Build the application:

```bash
./mvnw clean package
```

Build the Docker image:

```bash
docker build -t country-service .
```

Run the container:

```bash
docker run -p 8082:8082 country-service
```

## Academic Project

This project was developed collaboratively as part of our academic engineering studies, with the objective of applying backend development concepts, RESTful API design, database integration, automated testing and DevOps practices using the Spring ecosystem.

---
