# Database Schema Documentation

## Overview

This document defines the database schema for the app, including tables, relationships, and key fields. The database is designed to store user data, video metadata, AI-generated ideas, and chat history.

---

## Database Technology

- **Database:** PostgreSQL (relational database).
- **ORM:** TypeORM (for managing database interactions).

---

## Tables

### 1. **Users Table**

- **Purpose:** Store user information and authentication details.
- **Fields:**
  - `id` (UUID): Primary key.
  - `email` (string): User’s email address (unique).
  - `password` (string): Hashed password (for email/password login).
  - `createdAt` (timestamp): Account creation date.
  - `updatedAt` (timestamp): Last updated date.

### 2. **Videos Table**

- **Purpose:** Store video metadata fetched from the YouTube API.
- **Fields:**
  - `id` (UUID): Primary key.
  - `videoId` (string): YouTube video ID (unique).
  - `title` (string): Video title.
  - `thumbnail` (string): URL of the video thumbnail.
  - `viewCount` (number): Number of views.
  - `uploadDate` (timestamp): Video upload date.
  - `transcript` (text): Video transcript (if available).
  - `createdAt` (timestamp): Record creation date.
  - `updatedAt` (timestamp): Last updated date.

### 3. **Ideas Table**

- **Purpose:** Store AI-generated ideas based on video analysis.
- **Fields:**
  - `id` (UUID): Primary key.
  - `userId` (UUID): Foreign key referencing the `Users` table.
  - `videoId` (UUID): Foreign key referencing the `Videos` table.
  - `idea` (text): AI-generated idea.
  - `createdAt` (timestamp): Idea creation date.
  - `updatedAt` (timestamp): Last updated date.

### 4. **Chats Table**

- **Purpose:** Store chat history between the user and the LLM.
- **Fields:**
  - `id` (UUID): Primary key.
  - `userId` (UUID): Foreign key referencing the `Users` table.
  - `message` (text): User’s message.
  - `response` (text): LLM-generated response.
  - `createdAt` (timestamp): Chat creation date.
  - `updatedAt` (timestamp): Last updated date.

---

## Relationships

### 1. **Users ↔ Videos**

- **Relationship:** One-to-Many.
- **Description:** A user can analyze multiple videos, but each video analysis is tied to a single user.

### 2. **Users ↔ Ideas**

- **Relationship:** One-to-Many.
- **Description:** A user can generate multiple ideas, but each idea is tied to a single user.

### 3. **Videos ↔ Ideas**

- **Relationship:** One-to-Many.
- **Description:** A video can have multiple ideas generated from it, but each idea is tied to a single video.

### 4. **Users ↔ Chats**

- **Relationship:** One-to-Many.
- **Description:** A user can have multiple chat interactions, but each chat is tied to a single user.

---

## Indexing

### 1. **Users Table:**

- Index on `email` for fast lookups during login.

### 2. **Videos Table:**

- Index on `videoId` for fast lookups during video analysis.

### 3. **Ideas Table:**

- Index on `userId` and `videoId` for efficient querying of user-specific ideas.

### 4. **Chats Table:**

- Index on `userId` for efficient querying of user-specific chat history.

---

## Example Queries

### 1. **Fetch User by Email:**

```sql
SELECT * FROM users WHERE email = 'user@example.com';
```

### 2. **Fetch Videos by Keyword:**

```sql
   SELECT \* FROM videos WHERE title ILIKE '%keyword%';
```

### 3. **Fetch Ideas for a User:**

```sql
   SELECT \* FROM ideas WHERE userId = 'user-uuid';
```

### 4. **Fetch Chat History for a User:**

```sql
   SELECT \* FROM chats WHERE userId = 'user-uuid' ORDER BY createdAt DESC;
```

---

## Migrations

- **Purpose**: Manage schema changes over time.

- **Tools**: TypeORM migrations.

- **Example Migration**:

```typescript
import { MigrationInterface, QueryRunner } from "typeorm";

export class CreateUsersTable1712345678901 implements MigrationInterface {
  public async up(queryRunner: QueryRunner): Promise<void> {
    await queryRunner.query(`     CREATE TABLE users (
        id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
        email VARCHAR(255) UNIQUE NOT NULL,
        password VARCHAR(255) NOT NULL,
        createdAt TIMESTAMP DEFAULT NOW(),
        updatedAt TIMESTAMP DEFAULT NOW()
      );
  `);
  }

  public async down(queryRunner: QueryRunner): Promise<void> {
    await queryRunner.query(`DROP TABLE users;`);
  }
}
```
