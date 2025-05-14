
# UniverBoard - Integrated Campus Platform

## 1. Overview

UniverBoard is a comprehensive digital platform designed to manage university affairs, catering to students, faculty, college administration, and higher university management. Specifically tailored for institutions like Taiz University, it aims to enhance the educational and administrative experience through seamless digital integration. The platform provides distinct systems for various user roles, ensuring a tailored and efficient experience for each.

## 2. Core Features

*   **Student Portal:**
    *   User Authentication (Login/Registration)
    *   Personalized Dashboard
    *   Timetable Viewing
    *   Course Enrollment & Access to Materials (documents, videos, links)
    *   Assignment Submission & Tracking
    *   Grade Viewing
    *   Notifications (academic and system-wide)
    *   AI-Powered Study Planner
    *   User Directory (students and faculty)
    *   Profile Management

*   **College Administration Panel (`/admin/college`):**
    *   **Dashboard:** Key statistics (student enrollment, active courses, faculty count), list of urgent tasks, notifications, and quick links to management sections.
    *   **Manage Academic Programs:** View, create, and modify academic degree programs, including curriculum details and course linking.
    *   **Manage Courses:** Add, update, and delete courses, define course details (code, credit hours, prerequisites), and assign them to programs and semesters.
    *   **Manage Semesters & Sections:** Define academic semesters, create course sections, assign instructors, and manage class schedules and capacities.
    *   **Manage Students & Teachers:** View user lists, update profiles, manage enrollments/assignments, and handle manual registration or account issues for college-specific users.
    *   **Manage Reports & Statistics:** Generate various academic and administrative reports (e.g., enrollment trends, course completion rates, faculty workload).
    *   **Manage Announcements:** Create, schedule, and publish announcements targeted at specific groups within the college (e.g., all students, faculty of a department).
    *   **Manage User Permissions:** Define roles specific to the college (e.g., department head) and assign permissions to staff for accessing and managing relevant parts of the system.

*   **Super Administration Panel (`/admin/super`):**
    *   **Dashboard:** System-wide statistics (total users, managed colleges), system activity levels, critical notifications, and audit log summaries. Includes quick links to all super admin tools.
    *   **Manage System Users:** View all users across the system, create new accounts (students, faculty, staff), manage global permissions, and perform bulk actions.
    *   **Manage Colleges & Departments:** Create new colleges, define departments within them, and manage the university's organizational structure and hierarchies.
    *   **Manage Roles & Permissions:** Create custom global roles (e.g., "Librarian", "IT Support") and assign granular permissions controlling access to system features and data.
    *   **Publish System-Wide Announcements:** Draft and disseminate important messages to all users or target specific broad categories (e.g., all students, all faculty).
    *   **Manage Backups & Restores:** Monitor automated backup processes, manually trigger backups, view backup history, and access data restoration tools.
    *   **System Performance Monitoring:** View dashboards with Key Performance Indicators (KPIs), server health, database load, API response times, and generate reports on system usage.

## 3. Technology Stack

*   **Frontend:** Next.js (App Router, React 18, TypeScript)
*   **UI Components:** ShadCN UI
*   **Styling:** Tailwind CSS, CSS Variables for Theming (Light/Dark Mode)
*   **State Management:** React Context (primarily for Language and Theme)
*   **AI Integration:** Genkit (for features like the AI Study Planner, utilizing Google AI models like Gemini)
*   **Internationalization (i18n):** Custom Language Context supporting English (LTR) and Arabic (RTL)
*   **Firebase Services:**
    *   **Firestore:** Primary NoSQL database for application data.
    *   **Firebase Authentication:** For user sign-up and login.
    *   **Firebase Storage:** For storing user-uploaded files (e.g., profile pictures, course materials).
    *   **(Potentially) Firebase Cloud Messaging (FCM):** For push notifications (implied by notification features).
*   **Font:** Cairo (for both English and Arabic text)

## 4. Project Structure

*   `src/app/`: Main application routes using Next.js App Router.
    *   `(main)/`: Routes for general users (e.g., `/`, `/courses`, `/profile`). (Convention, not an actual folder named `(main)`)
    *   `admin/college/`: Routes for the College Administration Panel.
    *   `admin/super/`: Routes for the Super Administration Panel.
    *   `login/`, `register/`: Authentication pages.
*   `src/components/`: Reusable React components.
    *   `ui/`: ShadCN UI components.
    *   Custom components like `course-list.tsx`, `nav-menu.tsx`, `study-planner-form.tsx`, etc.
*   `src/ai/`: Genkit related code for AI features.
    *   `flows/`: Definitions of AI flows (e.g., `study-planner.ts`).
    *   `genkit.ts`: Global Genkit configuration and `ai` object initialization.
*   `src/context/`: React Context providers, notably `language-context.tsx`.
*   `src/hooks/`: Custom React hooks like `use-toast.ts` and `use-mobile.ts`.
*   `src/lib/`: Utility functions (`utils.ts`) and Firebase initialization (`firebase.ts`).
*   `src/types/`: TypeScript type definitions, especially `firestore.ts` for database models.
*   `public/`: Static assets. Any images placed here are served directly (e.g., `/Taizz_University_Logo.jpg`).
*   `.env`: Environment variables (ignored by Git, requires manual setup).
*   `next.config.ts`: Next.js specific configurations, including image optimization remote patterns.
*   `tailwind.config.ts`: Tailwind CSS theme and plugin configurations.
*   `src/app/globals.css`: Global styles, Tailwind base/components/utilities, and ShadCN CSS Variables for theming.
*   `components.json`: ShadCN UI configuration.

## 5. Getting Started

### Prerequisites

*   Node.js (LTS version recommended, check `engines` in `package.json` if specified)
*   npm or yarn package manager

### Firebase Setup

1.  Create a Firebase project at [https://console.firebase.google.com/](https://console.firebase.google.com/).
2.  In your Firebase project, enable the following services:
    *   **Firestore Database:** Start in test mode for initial development or configure security rules.
    *   **Authentication:** Enable Email/Password sign-in method, and any other methods you plan to use.
    *   **Storage:** Set up Firebase Storage for file uploads.
3.  Navigate to Project Settings > General in your Firebase console.
4.  Under "Your apps", register a new Web app.
5.  Copy the Firebase SDK configuration object (apiKey, authDomain, projectId, etc.).
6.  Create a `.env` file in the root of your project (if it doesn't exist) and populate it with your Firebase credentials:
    ```env
    NEXT_PUBLIC_FIREBASE_API_KEY=YOUR_API_KEY
    NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=YOUR_AUTH_DOMAIN
    NEXT_PUBLIC_FIREBASE_PROJECT_ID=YOUR_PROJECT_ID
    NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=YOUR_STORAGE_BUCKET
    NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=YOUR_MESSAGING_SENDER_ID
    NEXT_PUBLIC_FIREBASE_APP_ID=YOUR_APP_ID
    # Optional: NEXT_PUBLIC_FIREBASE_MEASUREMENT_ID=YOUR_MEASUREMENT_ID
    ```
    Replace `YOUR_...` placeholders with your actual Firebase project values.
7.  **Genkit AI Setup (for AI Study Planner):**
    *   The project uses Genkit with `@genkit-ai/googleai`. You'll need to have a Google AI API key (for Gemini models).
    *   Set up authentication for Google AI services. This typically involves setting the `GOOGLE_API_KEY` environment variable or configuring Application Default Credentials if running in a Google Cloud environment. Refer to the Google AI and Genkit documentation for detailed setup.
    *   The `.idx/integrations.json` file signifies that Project IDX has detected a Gemini API integration, which usually handles API key setup within the IDX environment. If running locally outside IDX, ensure the API key is accessible.

### Installation

Clone the repository and install the dependencies:

```bash
# If using npm
npm install

# If using yarn
yarn install
```

### Running the Development Server

To start the Next.js development server:

```bash
npm run dev
# or
yarn dev
```
The application will typically be available at `http://localhost:9002` (or the port specified in your `package.json` scripts).

To run the Genkit development server (for testing AI flows like the Study Planner):

```bash
npm run genkit:dev
# or
yarn genkit:dev
```
This usually starts the Genkit server on `http://localhost:4000`, providing a UI to inspect and run flows.

### Building for Production

```bash
npm run build
# or
yarn build
```

### Starting the Production Server

```bash
npm run start
# or
yarn start
```

## 6. Key Architectural Concepts

*   **Next.js App Router:** The application uses the App Router paradigm, emphasizing Server Components for performance and allowing Client Components (`'use client'`) for interactivity.
*   **Component-Based Architecture:** The UI is built using reusable React components, with ShadCN UI providing a base set of accessible and stylable components.
*   **Styling with Tailwind CSS & CSS Variables:** Utility-first styling is achieved with Tailwind CSS. The overall theme (colors, radius) is managed via CSS variables defined in `src/app/globals.css`, making theme customization (light/dark) straightforward.
*   **Internationalization (i18n):** The `LanguageProvider` in `src/context/language-context.tsx` enables dynamic language switching between English (LTR) and Arabic (RTL). It provides a `t` function for translating static text based on a dictionary of translation keys.
*   **AI Integration with Genkit:** Features like the "AI Study Planner" are implemented as Genkit flows. These are server-side TypeScript functions that can call Large Language Models (LLMs). They are invoked from client-side components as server actions.
*   **Client-Side State Management:** Primarily uses React's built-in state (`useState`, `useEffect`) and context (`useContext`) for managing local component state and global concerns like language and theme.
*   **Error Handling:** Uses `error.js` boundary files for route segments (Next.js convention) and toast notifications (`useToast`) for user feedback.
*   **Firebase Backend:**
    *   **Firebase Authentication:** Handles user sign-up, login, and identity management.
    *   **Firestore Database:** Serves as the primary NoSQL database for application data. Key collections include (refer to `src/types/firestore.ts` for detailed field definitions):
        *   `users`: Stores profiles for all users (students, teachers, admins).
            *   Fields typically include: `name`, `email`, `role` (`student`, `teacher`, `college_admin`, `super_admin`), `profileImageUrl`, `languagePreference`, `themePreference`.
            *   Student-specific fields: `studentNumber`, `departmentId`, `academicLevel`.
            *   Teacher-specific fields: `teacherRank`, `departmentId` (can be department name), `officeHours`.
        *   `courses`: Contains details for academic courses.
            *   Fields typically include: `courseNameEn`, `courseNameAr`, `code`, `teacherId` (references a user ID), `teacherName` (denormalized), `semester`, `creditHours`, `departmentId`.
            *   Subcollections (conceptual, structure depends on query needs and can be flatter or nested):
                *   `materials` (within each course document, or as a subcollection): For `CourseMaterial` items (files, links, videos).
                *   `assignments` (within each course document, or as a subcollection): For `Assignment` items.
                    *   `submissions` (subcollection of assignments, or a top-level collection linking student and assignment): For `Submission` items.
                *   `quizzes` (within each course document, or as a subcollection): For `Quiz` items.
                    *   `attempts` (subcollection of quizzes, or a top-level collection linking student and quiz): For `QuizAttempt` items.
                *   `announcements`: Course-specific announcements. (These might be part of the `notifications` collection, filtered by course context, or a dedicated subcollection under `courses`).
        *   `notifications`: Stores system-wide and course-specific notifications for users. (Matches the `Notification` type structure).
        *   _(Future)_ `messages`: Would store direct messages between users. (Not yet fully implemented in UI/types).
        *   _(Future)_ `academic_programs`: Would define degree programs, curricula, and link to `courses`.
        *   _(Future)_ `colleges`: Would define the university's organizational structure like colleges and departments.
    *   **Firebase Storage:** Used for storing user-uploaded files, such as profile pictures, course materials (PDFs, videos), and assignment submissions.
    *   **(Potentially) Firebase Cloud Messaging (FCM):** Implied by notification features; would be used for push notifications to client devices.

## 7. Design and Visual Identity

*   **Color Palette (Light Theme):**
    *   Background: `hsl(210 60% 98%)` (Very Light Blue-Gray)
    *   Foreground: `hsl(220 25% 25%)` (Dark Desaturated Blue)
    *   Primary: `hsl(220 70% 45%)` (Stronger Navy Blue)
    *   Secondary: `hsl(160 60% 40%)` (Teal Green)
    *   Accent: `hsl(190 65% 75%)` (Light Cyan Blue)
*   **Color Palette (Dark Theme):**
    *   Background: `hsl(220 35% 10%)` (Very Dark Navy/Slate)
    *   Foreground: `hsl(210 30% 92%)` (Light Grayish Blue)
    *   Primary: `hsl(210 75% 60%)` (Brighter Blue)
    *   Secondary: `hsl(160 55% 50%)` (Brighter Teal Green)
    *   Accent: `hsl(190 60% 55%)` (Medium Cyan Blue)
*   **Sidebar Theme:** Uses distinct background/foreground colors for contrast, derived from the main palette (e.g., dark navy or teal for light mode sidebar, very dark base for dark mode sidebar).
*   **Font:** The "Cairo" font is used for both English and Arabic text, ensuring visual consistency.
*   **Icons:** Lucide React icons are used throughout the application for a clean and modern look.
*   **Layout:** Responsive design principles are applied, with components adapting to different screen sizes. The sidebar is collapsible and adapts for mobile views.

## 8. Future Enhancements (Scalability)

*   **Laravel Backend Integration:** The initial project description mentioned a Laravel RESTful API. This could be integrated for more complex backend logic, business rules, or to serve as a primary API layer if Next.js is used more as a BFF (Backend For Frontend).
*   **Advanced Reporting & Analytics:** Building out the "Manage Reports & Statistics" sections with actual data visualization and generation capabilities (e.g., using `recharts` with real data).
*   **Real-time Features:** Expanding the use of Firebase Realtime Database or Firestore listeners for more dynamic, real-time updates in areas like messaging, collaborative features, or live notifications.
*   **Quiz System Implementation:** Developing the UI and full functionality for creating, taking, and grading quizzes based on the `Quiz` types defined in `src/types/firestore.ts`.
*   **Messaging System:** Building out the UI and backend logic for the direct messaging feature.
*   **Comprehensive Testing:** Implementing unit, integration, and end-to-end tests.
*   **Accessibility (A11y) Enhancements:** Continuous review and improvement of accessibility based on WCAG guidelines.

## 9. Contribution

This section can be expanded if the project becomes open source or involves multiple developers, detailing coding standards, branch strategies, and pull request processes.

link of project UniverBoard app system:
https://9000-firebase-studio-1747079312301.cluster-jbb3mjctu5cbgsi6hwq6u4btwe.cloudworkstations.dev
