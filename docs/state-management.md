# State Management Documentation

## Overview

This document outlines how state is managed in the app, including local state, global state, server state, and persistence. The goal is to ensure a consistent and efficient approach to state management across the app.

---

## Frontend State Management

### 1. **Local State**

- **Purpose:** Manage component-specific data (e.g., form inputs, UI toggles).
- **Tools:** React’s `useState` and `useReducer` hooks.
- **Examples:**
  - Form inputs (e.g., keyword search, chat messages).
  - UI toggles (e.g., dark mode, dropdown visibility).

### 2. **Global State**

- **Purpose:** Manage shared data across multiple components (e.g., user authentication status, trending videos).
- **Tools:** Zustand (lightweight and efficient state management library).
- **Examples:**
  - User authentication status (e.g., logged in, logged out).
  - Trending videos fetched from the backend.
  - AI-generated ideas and chat history.

### 3. **Server State**

- **Purpose:** Manage data fetched from the backend (e.g., video data, chat responses).
- **Tools:** React Query (for caching, synchronization, and background updates).
- **Examples:**
  - Video data fetched from the YouTube API.
  - Chat responses from the LLM.
  - Trending videos in specific categories.

### 4. **Persistence**

- **Purpose:** Persist state across sessions (e.g., user preferences, saved ideas).
- **Tools:** LocalStorage or Zustand middleware.
- **Examples:**
  - User preferences (e.g., dark mode, preferred categories).
  - Saved ideas for later reference.

---

## Backend State Management

### 1. **Session Management**

- **Purpose:** Manage user sessions and authentication.
- **Tools:** Clerk Authentication and JWT (JSON Web Tokens).
- **Examples:**
  - User login and session persistence.
  - Token-based authentication for protected API endpoints.

### 2. **Database State**

- **Purpose:** Manage persistent data stored in the database.
- **Tools:** PostgreSQL with TypeORM.
- **Examples:**
  - User profiles and preferences.
  - Video metadata and transcripts.
  - AI-generated ideas and chat history.

### 3. **Real-Time State**

- **Purpose:** Manage real-time data for the chat feature.
- **Tools:** Socket.IO.
- **Examples:**
  - Real-time chat messages between the user and the LLM.
  - Live updates for trending videos.

---

## State Management Flow

### Frontend Flow:

1. **Local State:**
   - Use `useState` or `useReducer` for component-specific data.
2. **Global State:**
   - Use Zustand to manage shared data across components.
3. **Server State:**
   - Use React Query to fetch and manage data from the backend.
4. **Persistence:**
   - Use LocalStorage or Zustand middleware to persist state across sessions.

### Backend Flow:

1. **Session Management:**
   - Use Clerk Authentication and JWT for secure user sessions.
2. **Database State:**
   - Use PostgreSQL with TypeORM to manage persistent data.
3. **Real-Time State:**
   - Use Socket.IO for real-time communication in the chat feature.

---

## Folder Structure

### Frontend:

src/
├── store/ # Zustand global state
│ ├── authStore.js # Authentication state
│ ├── videoStore.js # Video data state
│ ├── chatStore.js # Chat state
├── hooks/ # Custom React hooks
│ ├── useAuth.js # Authentication hook
│ ├── useVideos.js # Video data hook
│ ├── useChat.js # Chat hook
├── utils/ # Utility functions
│ ├── localStorage.js # LocalStorage utilities

### Backend:

src/
├── auth/ # Authentication module
│ ├── session.ts # Session management
├── database/ # Database module
│ ├── entities/ # TypeORM entities
│ ├── repositories/ # Database repositories
├── sockets/ # Socket.IO module
│ ├── chat.ts # Real-time chat state

---

## Examples

### Frontend: Zustand Store (authStore.js)

```javascript
import create from "zustand";

const useAuthStore = create((set) => ({
  isLoggedIn: false,
  user: null,
  login: (user) => set({ isLoggedIn: true, user }),
  logout: () => set({ isLoggedIn: false, user: null }),
}));

export default useAuthStore;
```

Frontend: React Query (useVideos.js)
import { useQuery } from 'react-query';
import axios from 'axios';

const fetchVideos = async (keyword) => {
const response = await axios.get(`/api/videos?keyword=${keyword}`);
return response.data;
};

const useVideos = (keyword) => {
return useQuery(['videos', keyword], () => fetchVideos(keyword));
};

export default useVideos;
Backend: Session Management (session.ts)
import { Injectable } from '@nestjs/common';
import { JwtService } from '@nestjs/jwt';

@Injectable()
export class SessionService {
constructor(private readonly jwtService: JwtService) {}

createToken(userId: string) {
return this.jwtService.sign({ userId });
}

verifyToken(token: string) {
return this.jwtService.verify(token);
}
}
