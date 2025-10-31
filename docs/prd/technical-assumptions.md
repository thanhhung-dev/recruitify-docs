# **Technical Assumptions**

**Repository Structure: Monorepo**
A monorepo will be used to manage both the frontend (Next.js) and backend (Spring Boot) code in a single repository.

**Service Architecture: Monolith**
For the MVP, a monolithic service architecture will be implemented. This approach is suitable for the initial feature set and allows for rapid development. The architecture should still be designed with modularity in mind to allow for potential future migration to microservices.

**Testing Requirements: Unit & Integration Testing**
All critical business logic in both the frontend and backend must be covered by unit tests. Integration tests should be written for key user workflows, such as user registration and application submission, to ensure the components work together correctly.

**Additional Technical Assumptions and Requests**
*   **Frontend:** Next.js with Ant Design for the component library.
*   **Backend:** Spring Boot (Java) to build the RESTful API.
*   **Database:** PostgreSQL will be the relational database.

---
