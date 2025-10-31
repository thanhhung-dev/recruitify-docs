# 19. Monitoring and Observability

### Monitoring Stack

We will use a combination of platform-native tools and third-party services to get a complete picture of our application's health.

*   **Frontend Monitoring:**
    *   **Vercel Analytics:** Will be used out-of-the-box to track Core Web Vitals, traffic sources, and page views.
    *   **Sentry (or similar):** Will be integrated to provide real-time frontend error tracking and performance monitoring of API calls from the client.
*   **Backend Monitoring:**
    *   **AWS CloudWatch:** Will be used to collect metrics, logs, and traces from our Spring Boot application running on ECS. We will set up dashboards to monitor CPU/Memory utilization, API latency, and error rates.
*   **Uptime Monitoring:**
    *   **UptimeRobot (or similar):** An external service will be configured to ping our primary frontend URL and a backend health-check endpoint every 5 minutes to alert us immediately of any downtime.

### Key Metrics to Watch

#### Frontend Metrics:

*   **Core Web Vitals (LCP, FID, CLS):** To measure the user's perceived loading, interactivity, and visual stability experience.
*   **JavaScript Error Rate:** The percentage of user sessions that encounter a JavaScript error.
*   **API Latency (Client-side):** The time it takes for API calls to resolve, as measured from the user's browser.

#### Backend Metrics:

*   **API Error Rate (5xx):** The percentage of server-side errors. A spike in this metric is a critical alert.
*   **API Latency (p95):** The 95th percentile response time for our API endpoints. This tells us the experience of the slowest 5% of requests.
*   **CPU & Memory Utilization:** The resource usage of our ECS container, to inform scaling decisions.
*   **Database Query Performance:** Monitoring for and optimizing slow database queries.
