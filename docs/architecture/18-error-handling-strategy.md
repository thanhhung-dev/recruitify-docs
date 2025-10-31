# 18. Error Handling Strategy

### Error Response Format

To ensure consistency, all errors returned by the backend API will follow a standardized JSON format. This allows the frontend to reliably parse and handle any error.

```typescript
// This interface will be defined in packages/shared-types
export interface ApiError {
  error: {
    code: string;          // A machine-readable error code (e.g., 'VALIDATION_ERROR')
    message: string;       // A developer-friendly error message
    details?: Record<string, any>; // Optional field for extra info (e.g., validation failures)
    timestamp: string;     // ISO 8601 timestamp of when the error occurred
  };
}
```

### Error Flow

This diagram shows how an error propagates from the backend to the frontend.

```mermaid
sequenceDiagram
    participant U as User
    participant FE as Web Frontend
    participant BE as API Service

    FE->>BE: Sends an invalid API request (e.g., bad data)
    activate BE
    BE->>BE: An exception is thrown (e.g., ValidationException)
    BE->>BE: A global exception handler catches it
    BE->>BE: Formats the exception into the standard ApiError object
    BE-->>FE: Responds with a 4xx/5xx status and the ApiError JSON body
    deactivate BE

    activate FE
    FE->>FE: API service layer catches the HTTP error
    FE->>FE: Extracts the ApiError object from the response
    FE->>FE: Updates a global state store with the error message
    FE-->>U: A user-friendly error message is displayed (e.g., a toast notification)
    deactivate FE
```

---
