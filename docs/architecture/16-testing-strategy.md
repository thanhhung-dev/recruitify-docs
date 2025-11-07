# 16. Testing Strategy

### The Testing Pyramid

Our testing strategy is based on a pyramid shape, which emphasizes having a large foundation of fast, isolated tests and a smaller number of slower, more integrated tests.

```
     / \
    / E2E \
   /_______
  /         \
 / Integration \
/_______________
/  Unit Tests   \
```

*   **Unit Tests (The Foundation):** These will be the most numerous tests in our codebase. They are small, fast, and test a single piece of code (like a React component or a Java service method) in isolation.
    *   **Backend:** Using **JUnit 5** and **Mockito**.
    *   **Frontend:** Using **Jest** and **React Testing Library**.
*   **Integration Tests (The Middle):** These tests verify that multiple components work together correctly. They are slightly slower and more complex than unit tests.
    *   **Backend:** Testing the interaction between controllers, services, and repositories (e.g., a full API request/response cycle).
    *   **Frontend:** Testing a component that uses a custom hook or interacts with a state store.
*   **End-to-End (E2E) Tests (The Peak):** These are the least numerous but most comprehensive tests. They simulate a real user's journey through the application in an actual browser.
    *   **Tool:** Using **Playwright**.
    *   **Example Flow:** A script that automates signing up, logging in, editing a profile, and applying for a job.

### Test Organization

*   **Frontend Tests (`apps/web`):** Unit and integration test files will be co-located with the code they are testing. For example, a test for `WorkExperienceCard.tsx` will be named `WorkExperienceCard.test.tsx` and live in the same directory.
*   **Backend Tests (`apps/api`):** Following standard Gradle convention, all tests will reside in the `src/test/java` directory, mirroring the package structure of the main source code.
*   **E2E Tests:** End-to-end tests written with Playwright will live in a separate, top-level `e2e/` directory at the root of the monorepo.

### Test Examples

#### Frontend Component Test Example (Jest & RTL)

This test verifies that a React component renders the correct data.

```typescript
// In apps/web/src/features/profile/WorkExperienceCard.test.tsx

it('should render the job title and company name', () => {
  const mockExperience = { jobTitle: 'Software Engineer', companyName: 'Recruitify', ... };
  render(<WorkExperienceCard experience={mockExperience} />);

  // Assert that the component correctly displays the passed-in data
  expect(screen.getByText('Software Engineer')).toBeInTheDocument();
  expect(screen.getByText('Recruitify')).toBeInTheDocument();
});
```

#### Backend Unit Test Example (JUnit 5 & Mockito)

This test verifies that a service method correctly calls its dependencies, without needing a real database.

```java
// In apps/api/src/test/java/com/recruitify/service/UserServiceTest.java

@Test
void whenRegisteringUser_itShouldHashThePassword() {
  // Given (Setup)
  RegisterUserDto dto = new RegisterUserDto("test@test.com", "password");
  when(userRepository.findByEmail(anyString())).thenReturn(Optional.empty());

  // When (Action)
  userService.register(dto);

  // Then (Verification)
  // Verify that the password hashing method was called exactly once
  verify(passwordEncoder, times(1)).encode("password");
  // Verify that the save method was called on the repository
  verify(userRepository, times(1)).save(any(User.class));
}
```

---

