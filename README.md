### Participants:
Felipe Maluli de Carvalho Dias - felipemcd1 (Insper email)<br>
Julia Karine Peres - juliakp1 (Insper email)

# Shikiri Microservices Project
This documentation serves as a central hub, detailing each microservice's functionality, API endpoints, and their interactions within the Shikiri ecosystem.

# Shikiri: Language Learning Platform

## Overview

Shikiri is a Trello-inspired platform, uniquely designed for language learning. It offers an interactive environment where users can efficiently organize and manage their language learning tasks on dedicated boards. From vocabulary revision to grammar practice, Shikiri facilitates a structured approach to language mastery.

Central to Shikiri's design is its ability to integrate various language learning tools directly into user tasks. This seamless incorporation of resources such as Anki decks for spaced repetition or listening practice tools provides a comprehensive and customized learning experience. By tailoring tasks to individual learning goals, Shikiri empowers users to create a personalized study plan that aligns with their aspirations, making the path to language proficiency both clear and engaging.

## Getting Started Locally

This section guides you through setting up Shikiri on your local machine. It assumes Docker is installed and running on your system. Follow these steps for a clean install, including service setup and resource package deployment.

### Prerequisites

Ensure you have the following installed:
- Docker
- Maven (for building Java projects)
- Git (for cloning repositories)

### Installation Steps

1. **Clone Repositories:**
   Begin by cloning the required Shikiri service repositories from GitHub.

2. **Build Services:**
   Navigate into each service directory and execute the following commands:
   - For compiling the service along with dependencies:
     ```shell
     mvn clean install
     ```
   - To package the service into a deployable JAR file:
     ```shell
     mvn clean package
     ```

3. **Deploy with Docker Compose:**
   Utilize Docker Compose in shikiri-docker-api or through ops to deploy Shikiri services, including any operational tools like Jenkins for CI/CD:

   ```shell
   docker compose up -d --build --force-recreate

    **IMPORTANT: Remember to add a .env file with the CONFIG and VOLUME chosen paths.


## Microservices Overview

### Account Service

- **Repositories:** 
  - [shikiri-account](https://github.com/FeMCDias/shikiri-account)
  - [shikiri-account-resource (package)](https://github.com/FeMCDias/shikiri-account-resource)
- **Description:** Handles user account operations including creation, login, and updates.
- **API Endpoints:**
  - `POST /accounts` - Create a new user account.
  - `POST /accounts/login` - User login.
  - `PUT /accounts/{id}` - Update user account.
  - `GET /accounts` - Retrieve user account details.
- **AccountIn Input Class**:
  - **Fields**:
    - `name`: String
    - `email`: String
    - `password`: String

### Authentication Service

- **Repositories:** 
  - [shikiri-auth](https://github.com/FeMCDias/shikiri-auth)
  - [shikiri-auth-resource (package)](https://github.com/FeMCDias/shikiri-auth-resource)
- **Description:** Manages authentication including user registration, login, and token validation.
- **API Endpoints:**
  - `POST /auth/register` - Register a new user.
  - `POST /auth/login` - Authenticate user and return a token.
  - `POST /auth/solve` - Token validation.
- **RegisterIn Input Class**:
  - **Fields**:
    - `name`: String
    - `email`: String
    - `password`: String
- **CredentialIn Input Class**:
  - **Fields**:
    - `email`: String
    - `password`: String
- **SolveIn Input Class**:
  - **Fields**:
    - `token`: String

### Discovery Service

- **Repository:** [shikiri-discovery](https://github.com/FeMCDias/shikiri-discovery)
- **Description:** Service registry for dynamic discovery and load balancing in the microservices architecture.

### Docker API Service

- **Repository:** [shikiri-docker-api](https://github.com/FeMCDias/shikiri-docker-api)
- **Description:** Provides Docker Compose configurations for deploying the microservices architecture.

### Gateway Service

- **Repository:** [shikiri-gateway](https://github.com/FeMCDias/shikiri-gateway)
- **Description:** Entry point for the architecture, routing requests to appropriate services.

### Operations Service

- **Repository:** [shikiri-ops](https://github.com/FeMCDias/shikiri-ops)
- **Description:** Focuses on monitoring, logging, and deployment strategies.

### Tasks Service

- **Repositories:** 
  - [shikiri-tasks](https://github.com/Juliakp1/shikiri-tasks)
  - [shikiri-tasks-resource (package)](https://github.com/Juliakp1/shikiri-tasks-resource)
- **Description:** Manages tasks, including creation, updates, and retrieval.
- **API Endpoints:**
  - `POST /tasks` - Create a task.
  - `PUT /tasks/{id}` - Update a task.
  - `GET /tasks` - Retrieve tasks.
- **TasksIn Input Class**:
  - **Fields**:
    - `name`: String
    - `description`: String
    - `tool`: String
    - `board`: String
    - `done`: Boolean

### Tool Service

- **Repositories:** 
  - [shikiri-tool](https://github.com/FeMCDias/shikiri-tool)
  - [shikiri-tool-resource (package)](https://github.com/FeMCDias/shikiri-tool-resource)
- **Description:** Handles tool operations and JWT authentication.
- **API Endpoints:**
  - `POST /tools/create` - Create a tool.
  - `PUT /tools/{id}` - Update a tool.
  - `DELETE /tools/{id}` - Delete a tool.
  - `GET /tools/{id}` - Retrieve a tool by ID.
  - `GET /tools/search/by-name-containing` - Find tools by name containing.
  - `GET /tools/search/by-category` - Find tools by category.
  - `GET /tools` - Find all tools sorted alphabetically.
- **ToolIn Input Class**:
  - **Fields**:
    - `name`: String
    - `category`: String
    - `description`: String
    - `userId`: String

### Board Service

- **Repositories:** 
  - [shikiri-board](https://github.com/Juliakp1/shikiri-board)
  - [shikiri-board-resource](https://github.com/Juliakp1/shikiri-board-resource)
- **Description:** The Board service facilitates the creation and management of boards, each containing tasks categorized by their progress status. Key categories include "Not Started", "In Progress", and "Done", enabling users to track their language learning activities effectively.
- **API Endpoints:**
  - `POST /boards` - Creates a new board.
  - `PUT /boards/{id}` - Updates an existing board.
  - `DELETE /boards/{id}` - Deletes a board.
  - `GET /boards/{id}` - Retrieves detailed information about a board.
  - `GET /boards/search/by-name` - Searches for boards by name containing.
  - `GET /boards` - Lists all boards.
- **BoardIn Input Class**:
   - **Fields**:
       - `title`: String
       - `description`: String
       - `categories`: List of `Category` Strings

## Additional Notes

- **JWT Authentication:** Certain endpoints require a valid JWT token in the `Authorization` header.
- **Error Handling:** Services implement error checking and handling for secure operation.

For more details on implementation, setup, and usage, please refer to the individual service repositories linked above.
