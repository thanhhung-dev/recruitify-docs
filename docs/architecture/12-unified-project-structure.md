# 12. Unified Project Structure

### Project Directory Structure

```
recruitify-client/
├── .github/
│   └── workflows/
│       └── ci.yaml             # CI/CD for frontend
│
├── src/
│   ├── components/             # UI components
│   ├── features/               # Feature modules (profile, jobs)
│   ├── pages/                  # Next.js routes
│   ├── services/               # API service layer
│   └── stores/                 # Zustand state stores
│
├── package.json
├── next.config.js
├── tsconfig.json
└── README.md

recruitify-server/
├── .github/
│   └── workflows/
│       └── ci.yaml             # CI/CD for backend
│
├── src/main/java/com/recruitify/
│   ├── controller/             # REST Controllers
│   ├── service/                # Business logic
│   ├── repository/             # JPA repositories
│   └── entities/               # Entity models
│
├── src/main/resources/
│   └── application.yml         # Config (DB, server port, etc.)
│
├── build.gradle
├── settings.gradle
└── README.md
```

---
