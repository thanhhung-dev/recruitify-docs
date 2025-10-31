# **Component Library / Design System**

**Design System Approach**
For the MVP, we will use an existing, comprehensive design system: **Ant Design**. This will ensure visual consistency, high-quality accessible components, and significantly faster development speed.

**Core Components**

**Component: Job Card**

- **Purpose:** To display a concise summary of a single job posting in a list format.
- **Usage Guidelines:** This will be used on the main Job Search Results page and the "Saved Jobs" page. The entire card will be a single link to the Job Details page. This will be built using the Ant Design `Card` or `List.Item` component.

**Component: Main Navigation Bar**

- **Purpose:** To provide persistent, top-level navigation throughout the application.
- **Variants:** The content of the navigation bar will change based on the user's role (Logged-Out, Job Seeker, Employer).
- **Usage Guidelines:** This will be implemented using the Ant Design `Layout.Header` and `Menu` components.

---
