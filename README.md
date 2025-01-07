# Project Name

## Overview

This project is a web app designed to help YouTube creators generate fresh video ideas by analyzing existing videos, transcripts, and titles using AI. The app also provides trending videos in specific categories and a chat feature for refining ideas.

---

## Features

- **Keyword Search:** Search for videos using keywords and optional filters.
- **Trending Videos:** Display trending videos in specific categories.
- **AI Analysis:** Analyze video transcripts and generate new ideas.
- **Chat Feature:** Refine ideas by chatting with the LLM.
- **Save/Export:** Save or export ideas in CSV format.
- **Authentication:** Secure login and sign-up using Clerk Authentication.

---

## Tech Stack

- **Frontend:** Next.js, Chakra UI, Tailwind CSS, Framer Motion, Zustand.
- **Backend:** NestJS, PostgreSQL, Socket.IO, Winston.
- **Third-Party APIs:** YouTube Data API, OpenAI API, Deepseek API, Clerk API.

---

## Getting Started

### Prerequisites

- Node.js (v16 or higher)
- PostgreSQL (v12 or higher)
- API keys for YouTube Data API, OpenAI API, Deepseek API, and Clerk API.

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/project-name.git
   ```
   Navigate to the project directory:
   cd project-name
   Install dependencies:
   npm install
   Set up environment variables:

Create a .env file in the root directory.

Add the following variables:
DATABASE_URL=postgres://user:password@localhost:5432/dbname
YOUTUBE_API_KEY=your-youtube-api-key
OPENAI_API_KEY=your-openai-api-key
DEEPSEEK_API_KEY=your-deepseek-api-key
CLERK_API_KEY=your-clerk-api-key
JWT_SECRET=your-jwt-secret
Running the App
Start the backend server:
npm run start:backend
Start the frontend development server:
npm run start:frontend
Open your browser and navigate to http://localhost:3000.
Documentation
Product Requirements Document (PRD)

Frontend Documentation

Backend Documentation

Third-Party Libraries Documentation

User Flow Documentation

State Management Documentation

Design Specification Document

Database Schema Documentation

API Documentation

Contributing
Fork the repository.

Create a new branch:
git checkout -b feature/your-feature-name
Commit your changes:

git commit -m "Add your feature"
Push to the branch:
git push origin feature/your-feature-name
Open a pull request.

License
This project is licensed under the MIT License. See the LICENSE file for details.

Acknowledgments
Next.js for the frontend framework.

NestJS for the backend framework.

Chakra UI and Tailwind CSS for styling.

YouTube Data API, OpenAI API, and Deepseek API for third-party integrations.
