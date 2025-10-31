# 17. Coding Standards

### Critical Fullstack Rules

1.  **Single Source of Truth for Types:** All types and interfaces shared between the frontend and backend (e.g., API responses) **MUST** be defined in the `packages/shared-types` directory. There should be no duplicate type definitions.
2.  **Use the Service Layer:** Frontend components **MUST NOT** make direct HTTP requests (e.g., using `axios` or `fetch`). They **MUST** call functions exported from the `services` layer (e.g., `profileService.getProfile()`).
3.  **Isolate Environment Variables:** Code **MUST NOT** access `process.env` directly. A dedicated configuration module should be created to parse, validate, and export environment variables to the rest of the application.
4.  **Immutable State:** Global state managed by Zustand **MUST NEVER** be mutated directly. Always use the `set` function within an action to produce a new state.

### Naming Conventions

| Element | Convention | Example |
| :--- | :--- | :--- |
| **Frontend** | | |
| React Components | `PascalCase` | `UserProfileCard.tsx` |
| React Hooks | `useCamelCase` | `useUserProfile.ts` |
| CSS Modules | `camelCase` | `styles.profileHeader` |
| **Backend** | | |
| Java Classes | `PascalCase` | `UserProfileService.java` |
| API Endpoints | `kebab-case` | `/api/v1/user-profiles` |
| Database Tables | `snake_case` | `user_profiles` |
| Database Columns | `snake_case` | `user_id`, `first_name` |

---
