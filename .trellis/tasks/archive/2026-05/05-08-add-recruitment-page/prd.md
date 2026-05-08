# Add Recruitment Page

## Goal

Add a recruitment (Join Us) page to the application to showcase career opportunities and attract talent.

## What I already know

* The user wants to add a recruitment page.
* The project uses Vue 3 (based on `App.vue`, `main.js`).
* There is a router (`src/router/index.js`) and views (`src/views/`).

## Assumptions (temporary)

* The page should be accessible via a link in the navigation (if any exists).
* The content will initially be static or placeholder information.

## Requirements

* **Company Introduction**: Section showcasing culture and why to join.
* **Job Listings**: A list of open positions (Frontend, Backend, Design) with titles and brief descriptions.
* **Application Form**: A reactive form for users to submit Name, Email, and Position. Includes basic validation and a "Success" alert on submit.
* **Route**: Add `/join` route to `src/router/index.js` using lazy loading.
* **Navigation**: Add "加入我们" link to the header in `src/App.vue`.
* **Styling**: Adhere to existing variables in `src/assets/main.css`.

## Acceptance Criteria

* [ ] Recruitment page is accessible at `/join`.
* [ ] Header has a working link "加入我们".
* [ ] Page includes an introduction section.
* [ ] Page displays a list of jobs.
* [ ] Application form validates inputs (email format, required fields).
* [ ] Form submission shows a "Success" notification (mocked).

## Technical Approach

* Create `src/views/JoinView.vue`.
* Use Vue 3 `<script setup>` syntax.
* Implement form state using `reactive`.
* Update `src/router/index.js` with the new route.
* Update `src/App.vue` template.

## Out of Scope

* Backend API integration for data persistence.
* Resume/File upload functionality.
* Mobile-specific CSS overrides (rely on global container scaling).

## Technical Notes

* **Framework**: Vue 3 (Composition API) with Vue Router.
* **Routes**: Defined in `src/router/index.js`.
* **Navigation**: Links are in `src/App.vue`.
* **Styling**: Global styles and variables in `src/assets/main.css`.
* **Conventions**:
    * Views are in `src/views/`.
    * Components are in `src/components/`.
    * Routes use lazy loading for new pages.
