# 6. Components

### Component: Web Frontend

**Responsibility:** This component is responsible for rendering the entire user interface and handling all user interactions in the browser. It fetches data from the backend API, manages client-side state, and presents a responsive, accessible, and performant experience to the user.

**Key Interfaces:**

*   **Pages/Routes:** Serves all user-facing pages, including `/` (Homepage), `/dashboard`, `/profile`, and job search pages.
*   **API Client:** Contains the logic for making authenticated requests to the backend API Service.

**Dependencies:**

*   **API Service:** Relies on the backend API for all data fetching and mutations.
*   **Authentication Service:** Depends on the backend for user authentication and session validation.
*   **External Auth Providers:** Interacts with Google/LinkedIn for social sign-on.

**Technology Stack:** Next.js, React, TypeScript, Ant Design, Zustand, NextAuth.js.

---


### Component: API Service

**Responsibility:** This component is the central backend monolith. It is responsible for implementing all business logic, processing data, and managing the application's state. It handles requests from the Web Frontend, enforces business rules, interacts with the database, and integrates with any external services.

**Key Interfaces:**

*   **REST API:** Exposes the secure REST API (defined in our OpenAPI specification) that the Web Frontend consumes. This is its sole interface with the outside world, accessed via the API Gateway.

**Dependencies:**

*   **Database Service (PostgreSQL):** For all data persistence and retrieval.
*   **File Storage Service (S3):** For storing and retrieving large binary files like resumes or profile pictures.
*   **External Auth Providers (Google/LinkedIn):** For validating social login tokens during the authentication process.

**Technology Stack:** Spring Boot, Java 17, Gradle, JUnit 5, Mockito.

---
