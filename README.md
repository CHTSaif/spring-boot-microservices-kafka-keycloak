
```markdown
# Spring Boot Microservices with Kafka and Keycloak

This project demonstrates a microservices architecture using Spring Boot, integrating Apache Kafka for messaging and Keycloak for authentication and authorization.

## Table of Contents

- [Architecture Overview](#architecture-overview)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
  - [1. Clone the Repository](#1-clone-the-repository)
  - [2. Start the Services](#2-start-the-services)
  - [3. Configure Keycloak Realm](#3-configure-keycloak-realm)
- [Microservices Overview](#microservices-overview)
- [Testing the Application](#testing-the-application)
- [Contributing](#contributing)
- [License](#license)

## Architecture Overview

The system comprises multiple microservices, each responsible for a specific domain. These services communicate asynchronously through Kafka topics. Security is enforced using Keycloak, providing centralized authentication and authorization. The infrastructure includes MySQL and MongoDB databases, managed through Docker containers.

## Prerequisites

- **Docker and Docker Compose**: Ensure that you have Docker and Docker Compose installed on your machine.

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/CHTSaif/spring-boot-microservices-kafka-keycloak.git
cd spring-boot-microservices-kafka-keycloak
```

### 2. Start the Services

Use Docker Compose to start all required services, including Kafka, Keycloak, MySQL, and MongoDB:

```bash
docker-compose up -d
```

This command will initialize the following services:

- **Kafka**: Message broker for inter-service communication.
- **Keycloak**: Identity and access management.
- **MySQL**: Relational database for persistent storage.
- **MongoDB**: NoSQL database for specific use cases.

### 3. Configure Keycloak Realm

1. **Access Keycloak Admin Console**: Navigate to `http://localhost:8181` in your browser.
2. **Log In**: Use the default credentials (`admin/admin` unless changed).
3. **Create a New Realm**: Click on "Add Realm" and name it `microservices-realm`.
4. **Create a Client**:
   - Navigate to the "Clients" section and click "Create".
   - Enter `spring-boot-client` as the Client ID.
   - Set the Access Type to `confidential`.
   - Save the client.
5. **Configure Client Credentials**:
   - After saving, navigate to the "Credentials" tab.
   - Note the Secret; this will be used by your microservices to authenticate with Keycloak.
6. **Define Roles**:
   - Navigate to the "Roles" section.
   - Create roles as needed (e.g., `USER`, `ADMIN`).
7. **Create Users**:
   - Navigate to the "Users" section and click "Add User".
   - Provide necessary details and save.
   - After saving, go to the "Credentials" tab to set a password.
   - Assign roles to the user under the "Role Mappings" tab.

## Microservices Overview

Each microservice is designed to handle specific business functionalities:

- **Account Command Service**: Manages account-related commands and processes, interacting with MongoDB for data persistence.
- **Account Query Service**: Handles account-related queries, retrieving data from MySQL.
- **User Service**: Manages user information and authentication, integrating with Keycloak for user management.

### Communication

- **Synchronous**: Services may use RESTful APIs for immediate requests and responses.
- **Asynchronous**: Kafka is utilized for events like account creation, updates, etc., ensuring decoupled and efficient communication.

## Testing the Application

1. **Obtain an Access Token**:
   - Use tools like Postman to authenticate against Keycloak.
   - Obtain a token by providing client credentials and user login details.
2. **Access Secure Endpoints**:
   - Include the obtained token in the `Authorization` header as a Bearer token when making API requests to the microservices.
3. **Verify Inter-Service Communication**:
   - Create an account using the Account Command Service API.
   - Query account details using the Account Query Service to ensure data consistency.
   - Monitor Kafka topics to verify that events are being published and consumed as expected.

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request for any enhancements, bug fixes, or documentation improvements.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```

This `README.md` provides a comprehensive guide to setting up and understanding the project. Adjust the content as necessary to fit the specific configurations and features of your project. 
