# 5. API Specification

### REST API Specification (OpenAPI 3.0)

```yaml
openapi: 3.0.0
info:
  title: Recruitify API
  version: 1.0.0
  description: The official API for the Recruitify platform.
servers:
  - url: /api/v1
    description: Version 1 of the Recruitify API

paths:
  /profile:
    get:
      summary: Get the current authenticated user's full profile
      tags: [Profile]
      responses:
        '200':
          description: The user's complete profile.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserProfile'
        '401':
          description: Unauthorized.

  /profile/work-experience:
    post:
      summary: Add a new work experience to the user's profile
      tags: [Profile]
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/WorkExperienceInput'
      responses:
        '201':
          description: The work experience was created successfully.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/WorkExperience'

  /profile/work-experience/{experienceId}:
    put:
      summary: Update an existing work experience
      tags: [Profile]
      parameters:
        - name: experienceId
          in: path
          required: true
          schema:
            type: string
            format: uuid
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/WorkExperienceInput'
      responses:
        '200':
          description: The updated work experience object.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/WorkExperience'

components:
  schemas:
    WorkExperience:
      type: object
      properties:
        id: { type: string, format: uuid }
        jobTitle: { type: string }
        companyName: { type: string }
        # ... other fields from the WorkExperience model

    WorkExperienceInput:
      type: object
      properties:
        jobTitle: { type: string }
        companyName: { type: string }
        # ... other fields, but excluding 'id'

    UserProfile:
      type: object
      properties:
        id: { type: string, format: uuid }
        email: { type: string, format: email }
        # ... all other fields from the UserProfile model
```

---
