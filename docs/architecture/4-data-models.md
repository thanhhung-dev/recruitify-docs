# 4. Data Models

### Model: User

**Purpose:** Represents an authenticated user in the system, holding core identity and security information. A `role` attribute will distinguish between Job Seekers and Recruiters.

**Key Attributes:**

*   `id`: `string` (UUID) - The unique primary key.
*   `email`: `string` - The user's unique email address for login.
*   `passwordHash`: `string` - The securely hashed password (never exposed via API).
*   `role`: `'JOB_SEEKER' | 'RECRUITER'` - The user's role in the system.
*   `createdAt`: `Date` - Timestamp of account creation.
*   `updatedAt`: `Date` - Timestamp of the last update.

**TypeScript Interface:**

```typescript
export interface User {
  id: string;
  email: string;
  role: 'JOB_SEEKER' | 'RECRUITER';
  createdAt: Date;
  updatedAt: Date;
}
```

**Relationships:**

*   A `User` with the `JOB_SEEKER` role has one `UserProfile`.
*   A `User` with the `RECRUITER` role has many `JobPostings`.

---


### Model: UserProfile

**Purpose:** Stores the detailed professional information for a `JOB_SEEKER`, separate from their core authentication data.

**Key Attributes:**

*   `userId`: `string` - A foreign key linking directly to the `User` model's `id`.
*   `firstName`: `string` - The user's first name.
*   `lastName`: `string` - The user's last name.
*   `headline`: `string` - A short, professional headline (e.g., "Senior Software Engineer").
*   `summary`: `string` - A longer "About Me" section.
*   `avatarUrl`: `string` - URL to the user's profile picture, stored in Amazon S3.

**TypeScript Interface:**

```typescript
import { User } from './user'; // Assuming types are co-located

export interface UserProfile extends User {
  firstName: string;
  lastName: string;
  headline: string;
  summary: string;
  avatarUrl: string;
  workExperiences: WorkExperience[];
  educations: Education[];
  skills: Skill[];
}
```

**Relationships:**

*   Belongs to one `User`.
*   Has many `WorkExperience` entries.
*   Has many `Education` entries.
*   Has many `Skills`.

---


### Model: WorkExperience

**Purpose:** Represents a single job or position within a user's professional history.

**Key Attributes:**

*   `id`: `string` (UUID) - The primary key.
*   `profileId`: `string` - Foreign key to the `UserProfile`.
*   `jobTitle`: `string`
*   `companyName`: `string`
*   `location`: `string` (e.g., "San Francisco, CA")
*   `startDate`: `Date`
*   `endDate`: `Date` (Can be null if it's the current job).
*   `description`: `string` - A summary of responsibilities and achievements.

**TypeScript Interface:**

```typescript
export interface WorkExperience {
  id: string;
  jobTitle: string;
  companyName: string;
  location: string;
  startDate: Date;
  endDate: Date | null;
  description: string;
}
```

**Relationships:**

*   Belongs to one `UserProfile`.

---


### Model: Education

**Purpose:** Represents a single entry in a user's education history.

**Key Attributes:**

*   `id`: `string` (UUID) - The primary key.
*   `profileId`: `string` - Foreign key to the `UserProfile`.
*   `schoolName`: `string`
*   `degree`: `string` (e.g., "Bachelor of Science")
*   `fieldOfStudy`: `string` (e.g., "Computer Science")
*   `startDate`: `Date`
*   `endDate`: `Date`
*   `description`: `string` - Notes on activities, awards, etc.

**TypeScript Interface:**

```typescript
export interface Education {
  id: string;
  schoolName: string;
  degree: string;
  fieldOfStudy: string;
  startDate: Date;
  endDate: Date;
  description: string;
}
```

**Relationships:**

*   Belongs to one `UserProfile`.

---


### Model: Skill

**Purpose:** Represents a distinct professional skill that can be associated with multiple users.

**Key Attributes:**

*   `id`: `string` (UUID) - The primary key.
*   `name`: `string` (e.g., "TypeScript", "Project Management") - Must be unique.

**TypeScript Interface:**

```typescript
export interface Skill {
  id: string;
  name: string;
}
```

**Relationships:**

*   Has a many-to-many relationship with `UserProfile`. A join table (`UserProfileSkills`) will be used to link users to their skills.

---
