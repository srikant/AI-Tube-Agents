# API Documentation

## Overview

This document defines the RESTful API endpoints for the app, including request/response formats, authentication, and error handling. The API is built using **NestJS** and follows RESTful principles.

---

## Base URL

- **Development:** `http://localhost:3000/api`
- **Production:** `https://api.yourdomain.com/api`

---

## Authentication

- **Method:** JWT (JSON Web Tokens) via Clerk Authentication.
- **Header:** Include the JWT token in the `Authorization` header.
  ```http
  Authorization: Bearer <token>
  ```

---

## Endpoints

1. Authentication
   a. - **Login**
   **Endpoint**: POST /auth/login

- **Purpose**: Authenticate a user and return a JWT token.

- **Request Body**:

```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

- **Response**:

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "user-uuid",
    "email": "user@example.com"
  }
}
```

b. **Sign Up**
**Endpoint**: POST /auth/signup

**Purpose**: Create a new user account and return a JWT token.

**Request Body**:

```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

- **Response**:

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "user-uuid",
    "email": "user@example.com"
  }
}
```

---

### 2. Videos

a. **Search Videos**

- **Endpoint**: GET /videos
- **Purpose**: Fetch videos based on a keyword search.
- **Query Parameters**:

  - keyword (string): The search keyword.
  - filters (optional): Filters like viewCount, uploadDate.

- _Response_:

```json
[
  {
    "id": "video-uuid",
    "videoId": "youtube-video-id",
    "title": "Video Title",
    "thumbnail": "https://thumbnail.url",
    "viewCount": 1000,
    "uploadDate": "2023-10-01T00:00:00Z"
  }
]
```

b. **Get Trending Videos**

- **Endpoint**: GET /videos/trending

- **Purpose**: Fetch trending videos in specific categories.
- **Query Parameters**:
  category (string): The category (e.g., gaming, tech, lifestyle).

**Response**:

```json
[
  {
    "id": "video-uuid",
    "videoId": "youtube-video-id",
    "title": "Trending Video Title",
    "thumbnail": "https://thumbnail.url",
    "viewCount": 5000,
    "uploadDate": "2023-10-01T00:00:00Z"
  }
]
```

---

3. **Ideas**
   a. **Analyze Video**

- **Endpoint**: POST /ideas/analyze

- **Purpose**: Analyze a video transcript and generate ideas.

- **Request Body**:

```json
{
  "videoId": "youtube-video-id"
}
```

- **Response**:

```json
[
  {
    "id": "idea-uuid",
    "idea": "AI-generated idea based on the video transcript."
  }
]
```

b. **Get User Ideas**

- **Endpoint**: GET /ideas

- **Purpose**: Fetch AI-generated ideas for a user.

- **Query Parameters**:

userId (string): The ID of the user.

- **Response**:

```json
[
  {
    "id": "idea-uuid",
    "idea": "AI-generated idea based on the video transcript.",
    "videoId": "youtube-video-id",
    "createdAt": "2023-10-01T00:00:00Z"
  }
]
```

---

4. **_Chat_**
   a. **Send Message**

- **Endpoint**: POST /chat

- **Purpose**: Send a user message to the LLM and receive a response.

- **Request Body**:

```json
{
  "userId": "user-uuid",
  "message": "How can I improve this idea?"
}
```

- **Response**:

```json
{
  "id": "chat-uuid",
  "message": "How can I improve this idea?",
  "response": "You can improve this idea by...",
  "createdAt": "2023-10-01T00:00:00Z"
}
```

b. **Get Chat History**

- **Endpoint**: GET /chat

- **Purpose**: Fetch chat history for a user.

- **Query Parameters**:

userId (string): The ID of the user.

- **Response**:

```json
[
  {
    "id": "chat-uuid",
    "message": "How can I improve this idea?",
    "response": "You can improve this idea by...",
    "createdAt": "2023-10-01T00:00:00Z"
  }
]
```

---

## Error Handling

1. **Error Responses**
   - **400 Bad Request**:
   ```json
   {
     "statusCode": 400,
     "message": "Invalid input data."
   }
   ```
   - **401 Unauthorized**:
   ```json
   {
     "statusCode": 401,
     "message": "Unauthorized. Please log in."
   }
   ```
   - **\*404 Not Found**:
   ```json
   {
     "statusCode": 404,
     "message": "Resource not found."
   }
   ```
   - **500 Internal Server Error**:
   ```json
   {
     "statusCode": 500,
     "message": "An unexpected error occurred."
   }
   ```
2. **Rate Limiting**
   - **Limit**: 100 requests per minute per user.
   - **Response**:
   ```json
   {
     "statusCode": 429,
     "message": "Too many requests. Please try again later."
   }
   ```
