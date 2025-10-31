# 3. Tech Stack

### Technology Stack Table

| Category | Technology | Version | Purpose | Rationale |
| :--- | :--- | :--- | :--- | :--- |
| **Frontend** | | | | |
| Frontend Language | TypeScript | 5.x | Type safety, scalability | Industry standard for modern web apps. |
| Frontend Framework | Next.js | 14.x | Full-stack React framework | Chosen in PRD; excellent performance and DX. |
| UI Component Library | Ant Design | 5.x | UI consistency, rapid development | Chosen in UI/UX Spec for its rich components. |
| State Management | Zustand | 4.x | Simple, lightweight global state | Avoids boilerplate of Redux; ideal for most apps. |
| **Backend** | | | | |
| Backend Language | Java | 17 (LTS) | Robust, performant, mature | A stable, long-term support version. |
| Backend Framework | Spring Boot | 3.x | Rapid backend development | Chosen in PRD; vast ecosystem. |
| API Style | REST | | Standard for web APIs | Simple, well-understood, and stateless. |
| **Data & Storage**| | | | |
| Database | PostgreSQL | 15.x | Relational data storage | Powerful, open-source, and reliable. |
| File Storage | Amazon S3 | | User uploads (avatars, resumes) | Scalable, durable, and cost-effective. |
| **Auth** | | | | |
| Authentication | NextAuth.js & Spring Security | | User login, session management | NextAuth for easy social logins; Spring Security for API. |
| **Testing** | | | | |
| Frontend Testing | Jest & React Testing Library | latest | Unit & component testing | Standard for React/Next.js applications. |
| Backend Testing | JUnit 5 & Mockito | latest | Unit & integration testing | Standard for the Java/Spring ecosystem. |
| E2E Testing | Playwright | latest | End-to-end browser testing | Modern, fast, and reliable cross-browser testing. |
| **DevOps** | | | | |
| CI/CD | Vercel & GitHub Actions | | Automated build, test, deploy | Vercel for FE, GitHub Actions for BE container. |
| IaC Tool | AWS CDK | latest | Infrastructure as Code | Define AWS infrastructure using TypeScript. |
| Monitoring | Vercel Analytics & AWS CloudWatch | | Performance and health monitoring | Native monitoring for our chosen platforms. |

---
