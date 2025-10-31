# 13. Development Workflow

### Local Development Setup

#### Prerequisites

A developer will need the following tools installed on their machine:
*   Node.js (v18 or later)
*   npm (v9 or later)
*   Java (JDK 17)
*   Gradle
*   Docker & Docker Compose

#### Initial Setup

After cloning the repository, the initial setup is straightforward:

```bash
# 1. Install all Node.js dependencies from the root
npm install

# 2. Start the PostgreSQL database using Docker
docker-compose up -d
```

#### Development Commands

We will define scripts in the root `package.json` to manage the development servers using Turborepo.

```bash
# Start both the frontend and backend concurrently
# This will be the primary command used for development.
npm run dev

# Start only the Next.js frontend application
npm run dev:web

# Start only the Spring Boot backend application
npm run dev:api

# Run all tests across the monorepo
npm run test
```

### Environment Configuration

We will use `.env` files to manage environment variables for local development. A template file named `.env.example` will be committed to the repository to serve as a guide.

#### Required Environment Variables (`.env.example`)

```bash
# =================================================
# Frontend Variables (copy to apps/web/.env.local)
# =================================================

# The full URL of the backend API service
NEXT_PUBLIC_API_URL=http://localhost:8080/api/v1

# --- NextAuth.js Configuration ---
# A long, randomly generated string for session encryption
NEXTAUTH_SECRET=
NEXTAUTH_URL=http://localhost:3000

# --- Social Logins ---
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
LINKEDIN_CLIENT_ID=
LINKEDIN_CLIENT_SECRET=


# =================================================
# Backend Variables (copy to apps/api/.env)
# =================================================

# --- Database Connection ---
DB_URL=jdbc:postgresql://localhost:5432/recruitify
DB_USERNAME=postgres
DB_PASSWORD=postgres

# --- JWT Configuration ---
# A long, randomly generated string for signing tokens
JWT_SECRET=
JWT_EXPIRATION_MS=86400000 # 24 hours

# --- AWS S3 Configuration for File Storage ---
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=
S3_BUCKET_NAME=
```

---
