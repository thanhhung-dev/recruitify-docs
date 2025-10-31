# **Epic List**

*   **Epic 1: Foundation & Core Job Seeker Experience.**
    *   **Goal:** Establish the foundational infrastructure of the application and deliver the core job search experience for the primary user (Job Seeker). This includes project setup, user registration/login, and the ability to search, view, and save jobs.
*   **Epic 2: Employer Functionality & Application Workflow.**
    *   **Goal:** Introduce the employer side of the platform and connect the two user types. This epic enables employers to post and manage jobs, and allows job seekers to submit applications.
*   **Epic 3: Dashboard & History.**
    *   **Goal:** Enhance the user experience by providing tools for management and tracking. This includes the job seeker's application history and the employer's dashboard for managing applicants.

---

### **Epic 1: Foundation & Core Job Seeker Experience**

**Goal:** Establish the foundational infrastructure of the application and deliver the core job search experience for the primary user (Job Seeker). This includes project setup, user registration/login, and the ability to search, view, and save jobs.

---

**Story 1.1: Project & Infrastructure Setup**

As a Dev Team,
I want a configured project structure and CI/CD pipeline,
so that we have a stable foundation for building and deploying the application.

**Acceptance Criteria**
1.  A monorepo is initialized containing both the Next.js frontend and Spring Boot backend applications.
2.  A basic CI/CD pipeline is configured to build and run tests for both applications upon code commits.
3.  The initial PostgreSQL database schema for users and jobs is created and managed via migration files.
4.  The frontend application can successfully fetch data from a backend health-check endpoint to verify connectivity.

---

**Story 1.2: Basic Job Seeker Registration & Login**

As a first-time visitor,
I want to register for an account and log in,
so that I can access personalized features of the platform.

**Acceptance Criteria**
1.  A user can navigate to a registration page with fields for email and password.
2.  Upon submitting the registration form, a new user record is created in the database.
3.  A user can navigate to a login page.
4.  Upon successful login with correct credentials, the user is authenticated and redirected to the homepage.
5.  Appropriate error messages are shown for invalid registration or login attempts (e.g., "User already exists," "Invalid credentials").

---

**Story 1.3: View Job Listings**

As any user,
I want to see a list of available jobs on the platform,
so that I can begin to explore opportunities.

**Acceptance Criteria**
1.  The homepage or a dedicated "Jobs" page displays a list of job postings.
2.  Each job in the list displays the job title, company name, and location.
3.  The backend provides a public (unauthenticated) API endpoint to fetch a paginated list of jobs.
4.  The database is seeded with sample job data for development and initial display purposes.

---

**Story 1.4: Search and Filter Job Listings**

As a job seeker,
I want to search for jobs by keyword and filter them by location and category,
so that I can quickly find opportunities relevant to me.

**Acceptance Criteria**
1.  The job listings page includes a text input for keyword searching.
2.  The page includes filter controls (e.g., dropdowns) for location and job category.
3.  Applying a search or filter updates the list of jobs displayed on the page without a full page reload.
4.  The backend API for fetching jobs supports filtering by keyword, location, and category.

---

**Story 1.5: View Job Details**

As a job seeker,
I want to click on a job to see its full description,
so that I can evaluate if it's a good fit.

**Acceptance Criteria**
1.  Clicking on any job item in the search results list navigates the user to a unique page for that job.
2.  The job detail page displays all relevant information, including title, company, location, and the full job description.
3.  The backend provides a public API endpoint to fetch a single job by its unique ID.

---

**Story 1.6: Save a Job**

As a logged-in job seeker,
I want to save a job to a personal list,
so that I can easily find and review it later.

**Acceptance Criteria**
1.  When viewing a job's detail page, a logged-in user is shown a "Save Job" button/icon.
2.  Clicking "Save Job" adds the job to that user's personal list of saved jobs.
3.  The button's appearance changes to indicate the job is saved (e.g., "Saved" or a filled-in icon).
4.  A logged-out user does not see the "Save Job" button.
5.  The backend provides an authenticated API endpoint to add or remove a job from a user's saved list.

---

### **Epic 2: Employer Functionality & Application Workflow**

**Goal:** Introduce the employer side of the platform and connect the two user types. This epic enables employers to post and manage jobs, and allows job seekers to submit applications.

---

**Story 2.1: Employer Registration & Company Profile**

As a hiring manager,
I want to register an employer account and create a basic company profile,
so that I can post jobs and represent my company on the platform.

**Acceptance Criteria**
1.  The registration flow allows a user to choose an "Employer" account type.
2.  An employer user is prompted to create a basic company profile (e.g., company name, website, brief description) after their first login.
3.  The system backend distinguishes between "Job Seeker" and "Employer" user roles, granting different permissions for each.
4.  The company profile information is saved and associated with the employer's user account.

---

**Story 2.2: Create a Job Posting**

As a logged-in employer,
I want to fill out a form to create and post a new job listing,
so that I can attract candidates to my open role.

**Acceptance Criteria**
1.  A logged-in employer can access a "Post a New Job" page.
2.  The page contains a form with all necessary fields for a job listing (e.g., title, location, category, salary, description).
3.  Upon successful form submission, a new job record is created in the database, linked to the employer's company.
4.  The newly created job becomes publicly visible on the main job listings page.

---

**Story 2.3: Employer Job Management Dashboard**

As a logged-in employer,
I want a dashboard where I can see and manage all the jobs I've posted,
so that I can maintain a clear view of my active listings.

**Acceptance Criteria**
1.  A logged-in employer has a dedicated "Dashboard" page.
2.  The dashboard displays a list of all jobs posted by that employer.
3.  Each job in the list displays its title, status (e.g., Active, Inactive), and a count of applicants.
4.  The employer can perform basic management actions from the dashboard, such as editing or deactivating a job post.

---

**Story 2.4: Apply for a Job**

As a logged-in job seeker,
I want to apply for a job directly through the platform,
so that I can easily and efficiently submit my candidacy.

**Acceptance Criteria**
1.  When viewing a job details page, a logged-in job seeker is shown a prominent "Apply" button.
2.  Clicking "Apply" presents a simple application form (e.g., fields for name, email, and a resume upload).
3.  Upon submission, an application record is created, linking the job seeker's profile, the job, and the submitted information.
4.  After applying, the button's state changes to "Applied" to prevent duplicate submissions.
5.  A user who is not logged in is prompted to log in or register when they click the "Apply" button.

---

**Story 2.5: View Job Applicants**

As a logged-in employer,
I want to view a list of applicants for each of my jobs,
so that I can begin the candidate review process.

**Acceptance Criteria**
1.  From the employer dashboard, clicking on a specific job posting navigates to a page listing all applicants for that role.
2.  The applicant list displays the name of each candidate and the date they applied.
3.  The employer can click on an individual applicant to view the details they submitted with their application (e.g., view their profile, download their resume).
4.  The backend provides a secure API endpoint for an employer to retrieve applicants only for jobs they own.

---

### **Epic 3: Dashboard & History**

**Goal:** Enhance the user experience by providing tools for management and tracking. This includes the job seeker's application history and the employer's dashboard for managing applicants.

---

**Story 3.1: Job Seeker "My Applications" Page**

As a logged-in job seeker,
I want a page where I can see all the jobs I have applied for and their status,
so that I can track my job search progress in one place.

**Acceptance Criteria**
1.  A logged-in job seeker can navigate to a "My Applications" page via their profile or a main navigation link.
2.  The page displays a list of all jobs the user has applied to.
3.  Each item in the list shows the job title, company name, the date the application was submitted, and the application's current status (e.g., "Applied," "Under Review").
4.  The backend provides a secure API endpoint to fetch the application history for the currently logged-in user.

---

**Story 3.2: Job Seeker "Saved Jobs" Page**

As a logged-in job seeker,
I want a dedicated page where I can view all the jobs I have saved,
so that I can easily review them and decide whether to apply.

**Acceptance Criteria**
1.  A logged-in job seeker can navigate to a "Saved Jobs" page.
2.  The page displays a list of all jobs the user has previously saved.
3.  The user can click on any job in the list to navigate to its full detail page.
4.  The user can remove a job from their saved list directly from this page.

---

**Story 3.3: Basic Employer Applicant Management**

As a logged-in employer,
I want to change the status of an applicant within my dashboard,
so that I can manage my hiring pipeline and track candidate progression.

**Acceptance Criteria**
1.  When viewing the list of applicants for a job, an employer can change the status for each applicant.
2.  The available status options are: "New," "Under Review," "Interview," and "Closed" (for hired or rejected).
3.  Changing the status updates the application record in the database.
4.  The applicant list on the employer's dashboard visually reflects the updated status for each candidate.

---

**Story 3.4: Job Seeker Application Status Visibility**

As a job seeker,
I want to see if the status of my application changes,
so that I have visibility into where I stand in the hiring process.

**Acceptance Criteria**
1.  When an employer updates an applicant's status (from Story 3.3), the new status is reflected on the job seeker's "My Applications" page.
2.  For the MVP, the system will not send email or push notifications for status changes.
3.  The status shown to the job seeker is a simplified, user-friendly version of the employer's internal status (e.g., "Interview" is displayed as "In Progress").
