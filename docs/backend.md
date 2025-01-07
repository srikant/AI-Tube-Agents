# Backend Documentation

## Overview

The backend of the app is built using **NestJS** for its modular architecture, TypeScript support, and scalability. It uses **PostgreSQL** as the database for structured data and integrates with third-party APIs like **YouTube Data API**, **OpenAI API**, and **Deepseek API**. The backend exposes **RESTful APIs** for seamless communication with the frontend and uses **Clerk Authentication** for secure user authentication. Real-time communication for the chat feature is handled using **Socket.IO**.

---

## Tech Stack

- **Framework:** NestJS (for modular architecture and TypeScript support).
- **Database:** PostgreSQL (for structured data and complex queries).
- **Authentication:** Clerk Authentication (via Clerk API) and JWT for token-based authentication.
- **Third-Party APIs:**
  - **YouTube Data API:** Fetch video data, metadata, and transcripts.
  - **OpenAI API:** Enhance the chat feature with advanced natural language processing.
  - **Deepseek API:** Analyze video transcripts and generate ideas.
- **Real-Time Communication:** Socket.IO (for real-time chat functionality).
- **Error Handling:** Winston or Pino (for logging and debugging).
- **Rate Limiting:** express-rate-limit or NestJS Rate Limiter (to prevent abuse).
- **Hosting:** Render or AWS Elastic Beanstalk (for backend hosting).
- **CI/CD:** GitHub Actions (for automated testing and deployment).
- **Monitoring:** Datadog or Sentry (for performance monitoring and error tracking).

---

## API Endpoints

### 1. **GET /videos**

- **Purpose:** Fetch videos based on a keyword search.
- **Parameters:**
  - `keyword` (string): The search keyword.
  - `filters` (optional): Filters like view count, upload date, etc.
- **Response:**
  - List of videos with metadata (e.g., title, thumbnail, view count).

### 2. **GET /trending**

- **Purpose:** Fetch trending videos in specific categories.
- **Parameters:**
  - `category` (string): The category (e.g., gaming, tech, lifestyle).
- **Response:**
  - List of trending videos with metadata.

### 3. **POST /analyze**

- **Purpose:** Analyze video transcripts and generate ideas.
- **Request Body:**
  - `videoId` (string): The ID of the video to analyze.
- **Response:**
  - AI-generated ideas based on the video transcript and metadata.

### 4. **POST /chat**

- **Purpose:** Send user messages to the LLM and receive responses.
- **Request Body:**
  - `message` (string): The user’s message.
  - `context` (optional): Additional context for the LLM.
- **Response:**
  - LLM-generated response.

### 5. **POST /auth**

- **Purpose:** Handle authentication with Clerk (if needed for custom flows).
- **Request Body:**
  - `token` (string): The authentication token from Clerk.
- **Response:**
  - User profile data or error message.

### 6. **POST /feedback**

- **Purpose:** Collect user feedback for improvement.
- **Request Body:**
  - `userId` (string): The ID of the user providing feedback.
  - `feedback` (string): The feedback message.
- **Response:**
  - Success or error message.

---

## Database Schema

### 1. **Users Table**

- `id` (UUID): Primary key.
- `email` (string): User’s email address.
- `createdAt` (timestamp): Account creation date.
- `updatedAt` (timestamp): Last updated date.

### 2. **Videos Table**

- `id` (UUID): Primary key.
- `videoId` (string): YouTube video ID.
- `title` (string): Video title.
- `thumbnail` (string): URL of the video thumbnail.
- `viewCount` (number): Number of views.
- `uploadDate` (timestamp): Video upload date.
- `transcript` (text): Video transcript (if available).

### 3. **Ideas Table**

- `id` (UUID): Primary key.
- `userId` (UUID): Foreign key referencing the user.
- `videoId` (UUID): Foreign key referencing the video.
- `idea` (text): AI-generated idea.
- `createdAt` (timestamp): Idea creation date.

### 4. **Chats Table**

- `id` (UUID): Primary key.
- `userId` (UUID): Foreign key referencing the user.
- `message` (text): User’s message.
- `response` (text): LLM-generated response.
- `createdAt` (timestamp): Chat creation date.

---

## Authentication

- **Clerk Authentication:** Integrated via Clerk API for secure user authentication.
- **JWT:** Used for token-based authentication when interacting with protected API endpoints.

---

## Error Handling

- Return specific error messages and HTTP status codes:
  - **400**: Bad Request (e.g., missing parameters).
  - **401**: Unauthorized (e.g., invalid token).
  - **404**: Not Found (e.g., invalid endpoint).
  - **500**: Internal Server Error (e.g., backend issues).
- Log errors using **Winston** or **Pino** for debugging and monitoring.

---

## Rate Limiting

- Use **express-rate-limit** or **NestJS Rate Limiter** to prevent abuse:
  - Limit requests per user (e.g., 100 requests per minute).

---

## Real-Time Communication

- **Socket.IO:** Used for real-time communication in the chat feature.

---

## DevOps

- **Hosting:**
  - **Frontend:** Vercel.
  - **Backend:** Render or AWS Elastic Beanstalk.
- **CI/CD:** GitHub Actions for automated testing and deployment.
- **Monitoring:** Datadog or Sentry for performance monitoring and error tracking.

---

## Folder Structure

src/
├── auth/ # Authentication module (Clerk integration)
├── videos/ # Video search and analysis module
├── chat/ # Chat feature module
├── users/ # User management module
├── database/ # Database schema and migrations
├── utils/ # Utility functions (e.g., error handling, logging)
├── constants/ # Constants (e.g., API endpoints, error messages)
└── main.ts # Entry point for the NestJS application

---

## Next Steps

1. Set up the **NestJS** project and configure **PostgreSQL**.
2. Implement the **API endpoints** and integrate third-party APIs.
3. Set up **Clerk Authentication** and **JWT** for secure user authentication.
4. Implement **Socket.IO** for real-time chat functionality.
5. Configure **rate limiting** and **error handling**.
6. Deploy the backend using **Render** or **AWS Elastic Beanstalk**.
