# HMCTS DTS Developer Challenge
A full-stack task management system developed for the HMCTS Digital Technology Services Developer Challenge. This system enables users to efficiently manage tasks through a modern web interface with full CRUD operations.

---

## Project Overview
This solution demonstrates modern full-stack development practices with a **Spring Boot REST API backend** and an **Express.js frontend**, designed for managing caseworker tasks in the legal services domain.

The application allows users to create, view, update, and delete tasks, with a focus on clean architecture, usability, and maintainability.

---

## Architecture
The system follows a **client-server architecture** with clear separation of concerns:

### Backend (Spring Boot)
- REST API exposing task management endpoints
- Layered architecture:
  - **Controller layer** - handles HTTP requests and responses
  - **Repository layer** - data access via Spring Data JPA
- Validation using Jakarta Bean Validation (`@NotNull`, `@NotBlank`)
- Uses `ResponseEntity` for explicit and meaningful HTTP responses

### Frontend (Express + Nunjucks)
- Server-side rendered UI using **Nunjucks templates**
- Styled using the **GOV.UK Design System**
- Uses **Axios** to communicate with the backend API
- Implements view models for formatting:
  - Task status (for example `TO_DO` -> `To do`)
  - Dates formatted for display

---

## Key Features
- **Complete Task Management**  
  Create, view, update, and delete tasks

- **Professional UI**  
  Built using the GOV.UK Design System to align with public sector standards

- **Robust Backend**  
  RESTful API with validation and structured error handling

- **Status Management**  
  Update task status dynamically via UI controls

- **Filtering**  
  Filter tasks by ID within the UI

- **Modern Architecture**  
  Clear separation of concerns and maintainable code structure

- **Database Integration**  
  Persistent storage using JPA/Hibernate

---

## Data Model
### Task
| Field | Type | Description |
|-------|------|-------------|
| id | Long | Unique identifier |
| title | String | Task title (required) |
| description | String | Task description |
| status | Enum | Task status (required) |
| dueDateTime | LocalDateTime | Due date and time (required) |

### TaskStatus Enum
- `TO_DO`
- `IN_PROGRESS`
- `DONE`

---

## API Endpoints
### Create Task

`POST /tasks`

- Returns: `201 Created`

#### Request Body Example
```json
{
  "title": "Prepare case summary",
  "description": "Review documents and prepare summary for hearing",
  "status": "TO_DO",
  "dueDateTime": "2026-04-10T14:00:00"
}
```
#### Response Body Example
```json
{
  "id": 1,
  "title": "Prepare case summary",
  "description": "Review documents and prepare summary for hearing",
  "status": "TO_DO",
  "dueDateTime": "2026-04-10T14:00:00"
}
```

### Get All Tasks

`GET /tasks`

- Returns: `200 OK`

#### Response Body Example
```json
[
  {
    "id": 1,
    "title": "Prepare case summary",
    "description": "Review documents and prepare summary for hearing",
    "status": "TO_DO",
    "dueDateTime": "2026-04-10T14:00:00"
  },
  {
    "id": 2,
    "title": "Contact claimant",
    "description": "Follow up regarding supporting evidence",
    "status": "IN_PROGRESS",
    "dueDateTime": "2026-04-12T09:30:00"
  }
]
```

### Get Task by ID

`GET /tasks/{id}`

- Returns: `200 OK` or `404 Not Found`

### Update Task Status

`POST /tasks/{id}/status?status=IN_PROGRESS`

- Returns: `200 OK` or `404 Not Found`

### Delete Task

`POST /tasks/{id}/delete`

- Returns: `204 No Content`

---

## Frontend Functionality
- Task list view with:
  - Inline **status update dropdown**
  - **Delete button** per task
- **Create task form** with validation feedback
- **Filter by task ID**
- Clean layout using the GOV.UK grid system
- Error handling surfaced to users

---

## Testing Strategy
### Integration Testing
- Uses `@SpringBootTest` and `@AutoConfigureMockMvc`
- Uses **MockMvc** to test API endpoints through the full Spring application context
- Verifies end-to-end behaviour across the controller and repository layers
- Runs against the test profile and validates both HTTP responses and database state
- Covers:
  - Task creation
  - Retrieval of single and multiple tasks
  - Validation failures
  - Status updates
  - Deletion

### Functional Testing
- Uses **RestAssured**
- Runs against a live application instance
- Tests full request and response flow
- Covers:
  - Task creation
  - Retrieval
  - Status updates
  - Deletion

---

## How to Run Locally
### Prerequisites

- Java 21
- Node.js (v18+ recommended)
- Yarn
- PostgreSQL or H2

### Backend Setup

```bash
git clone https://github.com/modonnell96/dts-developer-challenge-backend
cd dts-developer-challenge-backend
./gradlew build
./gradlew bootRun
```

Runs on: `http://localhost:4000`

### Frontend Setup

```bash
git clone https://github.com/modonnell96/dts-developer-challenge-frontend
cd dts-developer-challenge-frontend
yarn install
yarn start:dev
```

Runs on: `http://localhost:3010`

---

## Repositories

This project is split across two repositories:

- **Frontend**  
  <https://github.com/modonnell96/dts-developer-challenge-frontend>

- **Backend**  
  <https://github.com/modonnell96/dts-developer-challenge-backend>
