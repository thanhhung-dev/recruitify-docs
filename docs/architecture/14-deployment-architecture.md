# 14. Deployment Architecture

### Deployment Strategy

We will adopt a separate deployment strategy for the frontend and backend, leveraging the strengths of each hosting platform.

#### Frontend Deployment

*   **Platform:** **Vercel**
*   **Process:**
    1.  The GitHub repository will be connected to a Vercel project.
    2.  Every push to the `main` branch will automatically trigger a production deployment.
    3.  Every pull request will automatically receive its own unique "preview" deployment URL for testing and review before merging.
    4.  Vercel will handle the build process, deploy the static assets to its global Edge CDN, and manage the serverless functions for Next.js.

#### Backend Deployment

*   **Platform:** **AWS (via GitHub Actions)**
*   **Process:**
    1.  A CI/CD workflow will be defined in `.github/workflows/ci.yaml`.
    2.  On a push to the `main` branch, the GitHub Actions workflow will be triggered.
    3.  The workflow will:
        a. Build the Spring Boot application into a runnable JAR.
        b. Build a Docker image from a `Dockerfile` that contains the JAR.
        c. Push the new Docker image to **Amazon Elastic Container Registry (ECR)**.
        d. Trigger a service update in **Amazon Elastic Container Service (ECS)** to deploy the new container image using the **Fargate** launch type.

### CI/CD Pipeline (Backend)

The backend deployment will be managed by a GitHub Actions workflow. The following is a conceptual outline of the pipeline configuration.

```yaml
# .github/workflows/ci.yaml
name: Deploy API to Production

on:
  push:
    branches: [ "main" ] # Trigger on push to the main branch

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Build, tag, and push image to Amazon ECR
        # This step would use docker build, tag, and push commands
        # to get the new image into our container registry.

      - name: Deploy to Amazon ECS
        # This step would use the AWS CLI to update the ECS service
        # with the new container image definition, triggering a deployment.
```

### Environments

We will maintain three distinct environments to ensure a stable and reliable release process.

| Environment | Frontend URL | Backend URL | Purpose |
| :--- | :--- | :--- | :--- |
| **Development** | `http://localhost:3000` | `http://localhost:8080` | For developers to build and test on their local machines. |
| **Staging** | `staging.recruitify.app` | `api.staging.recruitify.app` | A mirror of production for final testing and QA before release. |
| **Production** | `www.recruitify.app` | `api.recruitify.app` | The live environment for end-users. |

---
