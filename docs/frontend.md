# Frontend Documentation

## Overview

The frontend of the app is built using **Next.js** for its performance and SEO benefits, with **Chakra UI** as the UI library for a clean, minimalistic, and dark mode-only design. The app features a **top navigation bar**, **Tailwind CSS** for styling, and **Zustand** for state management. It is fully responsive, ensuring a seamless experience across desktop and mobile devices.

---

## Tech Stack

- **Framework:** Next.js (for SSR, SSG, and routing).
- **UI Library:** Chakra UI (for pre-built components and dark mode support).
- **Styling:** Tailwind CSS (utility-first CSS for rapid development).
- **State Management:** Zustand (lightweight and efficient global state management).
- **Animations:** Framer Motion (for smooth page transitions and hover effects).
- **Authentication:** Clerk Authentication (for secure and seamless login).

---

## UI Components

### 1. **Top Navigation Bar**

- **Purpose:** Provides easy navigation between key sections of the app.
- **Components:**
  - **Logo:** App logo on the left.
  - **Links:** Home, Trending, Chat, and Profile.
  - **Search Bar:** A search input for keyword searches.
  - **Login/Sign-Up Button:** Integrated with Clerk Authentication.

### 2. **Keyword Search Form**

- **Purpose:** Allows users to search for videos using keywords and optional filters.
- **Components:**
  - **Search Input:** A text input for entering keywords.
  - **Filters:** Dropdowns or toggles for optional filters (e.g., view count, upload date).
  - **Search Button:** Triggers the search and displays results.

### 3. **Trending Videos Section**

- **Purpose:** Displays trending videos in specific categories (e.g., gaming, tech, lifestyle).
- **Components:**
  - **Category Tabs:** Tabs for switching between categories.
  - **Video Cards:** Displays video thumbnails, titles, and view counts.

### 4. **Chat Feature**

- **Purpose:** Allows users to refine AI-generated ideas by chatting with the LLM.
- **Components:**
  - **Chat Window:** Displays the conversation between the user and the LLM.
  - **Input Field:** A text input for user messages.
  - **Send Button:** Submits the user’s message to the LLM.

### 5. **Save/Export Feature**

- **Purpose:** Allows users to save or export ideas in CSV format.
- **Components:**
  - **Save Button:** Saves the current idea to the user’s profile.
  - **Export Button:** Exports the idea as a CSV file.

---

## Styling

- **Framework:** Tailwind CSS.
- **Design:** Dark mode only, with soft highlights (e.g., cyan, teal) for buttons and links.
- **Responsive Design:** Fully responsive layouts optimized for desktop and mobile devices.

---

## State Management

- **Local State:** Managed using React’s `useState` and `useReducer` hooks for component-specific data (e.g., form inputs, UI toggles).
- **Global State:** Managed using **Zustand** for shared data (e.g., user authentication status, trending videos, AI-generated ideas).

---

## Animations

- **Library:** Framer Motion.
- **Animations:**
  - **Page Transitions:** Fade-in and slide-in effects for page transitions.
  - **Hover Effects:** Subtle hover effects on buttons and links.

---

## Responsive Design

- **Approach:** Mobile-first design with Tailwind CSS’s responsive utilities.
- **Mobile-Specific Features:**
  - Collapsible menus for navigation.
  - Larger touch targets for buttons and links.
  - Optimized layouts for smaller screens.

---

## Authentication

- **Library:** Clerk Authentication.
- **Features:**
  - Email/password login.
  - Social login (e.g., Google).
  - Secure session management.

---

## Folder Structure

```md
src/
├── components/ # Reusable UI components
├── pages/ # Next.js pages
├── styles/ # Tailwind CSS and custom styles
├── store/ # Zustand global state
├── utils/ # Utility functions
├── hooks/ # Custom React hooks
└── constants/ # Constants (e.g., API endpoints)
```

---

## Next Steps

1. Implement the **Top Navigation Bar** and **Keyword Search Form**.
2. Integrate **Clerk Authentication** for login/sign-up.
3. Build the **Trending Videos Section** and **Chat Feature**.
4. Add **Framer Motion** animations for page transitions and hover effects.
5. Ensure the app is fully responsive using **Tailwind CSS**.
