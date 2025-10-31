# 10. Frontend Architecture

### Component Architecture

#### Component Organization

We will adopt a hybrid approach, separating generic, reusable UI components from larger, feature-specific components. This provides a clean, scalable, and maintainable structure.

```
apps/web/src/
├── components/
│   ├── ui/          # Generic, reusable UI components (e.g., Button, Card, Input)
│   └── layout/      # App layout components (e.g., Navbar, Footer, PageWrapper)
│
├── features/
│   ├── auth/        # Components related to authentication (e.g., LoginForm)
│   ├── profile/     # Components specifically for the User Profile feature
│   │   ├── WorkExperienceCard.tsx
│   │   ├── WorkExperienceForm.tsx
│   │   └── SkillTagInput.tsx
│   └── jobs/        # Components for job search, posting, etc.
│
├── pages/           # Next.js page routes (e.g., /profile, /dashboard)
│
└── ... (other folders like hooks, services, etc.)
```

### State Management Architecture

We will use **Zustand** for global state management, chosen for its simplicity, minimal boilerplate, and performance. We will structure our state into modular, feature-based stores.

#### State Structure

Our state will be divided into separate "stores" or "slices," each responsible for a specific domain of the application. This keeps stores small, focused, and easy to manage.

```
apps/web/src/stores/
├── useUserStore.ts     # Manages authenticated user data and session info
├── useProfileStore.ts  # Manages state for the user profile page (e.g., editing state)
└── useJobsStore.ts       # Manages state for job searches, filters, and results
```

#### State Management Patterns

*   **Async Actions:** API calls that modify global state will be encapsulated as async actions within the relevant store. For example, `useProfileStore` will have an action like `fetchUserProfile(userId)` that handles the API call and updates the store with the result.
*   **Computed State:** We will use selectors to derive values from the base state wherever possible (e.g., deriving a `user.isLoggedIn` boolean from the presence of a user object).
*   **Persistence:** We will use Zustand's `persist` middleware to save critical, non-sensitive state to `localStorage`, such as the user's session information, to keep them logged in across browser sessions.

### Routing Architecture

We will use the file-system based router built into Next.js. The structure of the `pages` directory will define the application's URL structure.

#### Route Organization

The `pages` directory will be organized logically, with dynamic routes used for specific resources like jobs.

```
apps/web/src/pages/
├── _app.tsx          # Global App component, wraps all pages
├── index.tsx         # Homepage route: /
├── login.tsx         # Login & Registration route: /login
│
├── dashboard.tsx     # Protected route: /dashboard
├── profile.tsx       # Protected route: /profile
│
└── jobs/
    ├── index.tsx     # Job search results route: /jobs
    └── [jobId].tsx   # Dynamic route for a single job: /jobs/some-job-id
```

#### Protected Route Pattern

To protect routes that require authentication (like `/dashboard` and `/profile`), we will create a wrapper component, for example, `<AuthGuard>`.

This component will wrap the page's content. It will check for the user's authentication status (e.g., by checking our `useUserStore`).

*   If the user **is authenticated**, it will render the page's content.
*   If the user **is not authenticated**, it will redirect them to the `/login` page.

This check will happen on the client-side. We can also add server-side checks in `getServerSideProps` for pages that require it, providing an additional layer of security.

### Frontend Services Layer

To keep our UI components clean and decoupled from the backend, we will create a dedicated "services layer." This layer will be responsible for all API communication. Components will never make direct HTTP requests; they will always go through this layer.

#### API Client Setup

We will create a single, centralized `axios` instance that will be used for all API requests. This instance will be configured with the API base URL and an interceptor to automatically attach the user's authentication token to every request.

```typescript
// located at services/apiClient.ts
import axios from 'axios';
import { useUserStore } from '@/stores/useUserStore';

const apiClient = axios.create({
  baseURL: process.env.NEXT_PUBLIC_API_URL || '/api/v1',
});

// Request interceptor to add the auth token
apiClient.interceptors.request.use((config) => {
  const token = useUserStore.getState().token;
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

export default apiClient;
```

#### Service Example

For each feature or data model, we will create a corresponding service file that uses the `apiClient` to export a set of functions.

```typescript
// located at services/profileService.ts
import apiClient from './apiClient';
import { UserProfile, WorkExperience } from '@/packages/shared-types';

export const profileService = {
  getProfile: async (): Promise<UserProfile> => {
    const response = await apiClient.get('/profile');
    return response.data;
  },

  addWorkExperience: async (data: Partial<WorkExperience>): Promise<WorkExperience> => {
    const response = await apiClient.post('/profile/work-experience', data);
    return response.data;
  },
};
```

---
