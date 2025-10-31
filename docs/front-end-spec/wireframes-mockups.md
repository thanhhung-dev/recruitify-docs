# **Wireframes & Mockups**

**Primary Design Files**
For the MVP, we will not create high-fidelity mockups for every screen in a design tool like Figma beforehand. Instead, to accelerate development, we will leverage the pre-built components and layout patterns from the **Ant Design** library. This specification, along with the user flows, will guide the developers in constructing the interface.

**Key Screen Layouts**

**Screen: Job Search Results Page**

- **Purpose:** To display a list of jobs matching the user's search criteria and allow for easy scanning and filtering.
- **Key Elements:**
  - **Left Sidebar (Filters):**
    - Keyword search input.
    - Location filter (e.g., text input or dropdown).
    - Category filter (e.g., multi-select checkboxes).
    - "Apply Filters" button.
  - **Main Content Area (Results):**
    - A heading indicating the number of results found (e.g., "Showing 78 jobs").
    - A list of "Job Cards".
    - Pagination controls at the bottom of the list.
- **Interaction Notes:**
  - Applying filters in the sidebar should update the main results list without a full page reload.
  - Clicking anywhere on a "Job Card" should navigate the user to the corresponding "Job Details Page".
- **Design File Reference:** To be built directly using Ant Design components.

---
