# 📚 LearnLens: Your AI-Powered Revision Assistant

**LearnLens transforms static PDF coursebooks into an interactive and personalized learning experience. By leveraging the power of Large Language Models, it generates dynamic quizzes, helps you track your progress, and turns passive reading into active revision.**

---

### **[✨ Live Demo URL ✨](https://your-learnlens-url.vercel.app)**

**(Note: Please add your Vercel deployment link here)**

![LearnLens Dashboard Screenshot](https://via.placeholder.com/800x400.png?text=Add+A+Screenshot+Of+Your+App+Dashboard)
*(Recommendation: Replace the placeholder above with an actual screenshot of your application)*

---

## 📖 Table of Contents

- [About The Project](#about-the-project)
- [Core Features](#core-features)
- [Tech Stack](#tech-stack)
- [The Development Journey: How LLMs Were Used](#the-development-journey-how-llms-were-used)
- [System Architecture](#system-architecture)
- [Getting Started (Local Setup)](#getting-started-local-setup)
- [Tradeoffs & Decisions](#tradeoffs--decisions)
- [Future Improvements](#future-improvements)

---

## 🎯 About The Project

The goal of this project was to build a fully functional, responsive web app to help students revise from their coursebooks within a tight deadline. The core challenge was to move quickly without sacrificing quality, which necessitated the aggressive use of LLMs as a development partner.

LearnLens addresses a common problem for students: passive learning. Simply re-reading a textbook is often ineffective. This application makes learning active by:
1.  Allowing students to use their own PDF coursebooks as a source of truth.
2.  Generating a variety of questions (MCQs, Short & Long Answer) directly from the content.
3.  Providing instant feedback, scoring, and explanations to reinforce concepts.
4.  Offering a dashboard to visualize progress and identify areas for improvement.

This project was built as part of the BeyondChats assignment, with a focus on demonstrating rapid prototyping, feature implementation, and making smart architectural decisions under pressure.

---

## ✨ Core Features

This section details the scope of the project as per the assignment, outlining what has been completed and what is planned for the future.

### ✅ Must-Have Features (Completed)

-   **[x] Source Selector & PDF Upload:** Users can select from pre-seeded NCERT Physics PDFs or securely upload their own coursebooks.
-   **[x] PDF Viewer:** An integrated, side-by-side PDF viewer allows users to reference the source material while taking a quiz.
-   **[x] AI Quiz Generator Engine:**
    -   Dynamically generates Multiple Choice (MCQs), Short Answer (SAQs), and Long Answer (LAQs) questions from the selected PDF's content.
    -   Renders a clean, interactive quiz interface.
    -   Captures user answers, provides instant scoring, and delivers detailed explanations for each question to aid understanding.
    -   Allows regenerating a new set of questions on demand.
-   **[x] Progress Tracking:**
    -   All quiz attempts, scores, and answers are stored securely per user.
    -   A simple yet effective dashboard visualizes the user's learning journey, including recent activity and average scores.

### ⏳ Nice-to-Have Features (Planned for Future)

-   **[ ] ChatGPT-style Chat UI:** A conversational interface for students to ask questions and get answers directly from their textbook content.
-   **[ ] RAG with Citations:** Implementing a Retrieval-Augmented Generation (RAG) pipeline to provide answers with direct quotes and page number citations from the source PDF.
-   **[ ] YouTube Video Recommender:** An engine to suggest relevant educational YouTube videos based on the topics present in the uploaded PDF.

---

## 🛠️ Tech Stack

The technology stack was chosen to prioritize development speed, scalability, and a modern user experience.

| Category             | Technology                                                                                                  | Reason for Choice                                                                            |
| -------------------- | ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **Framework** | [**Next.js 14**](https://nextjs.org/) (App Router)                                                          | Full-stack capabilities in one framework, simplifying the development of both front-end and back-end. |
| **Language** | [**TypeScript**](https://www.typescriptlang.org/)                                                          | Provides type safety, reducing bugs and improving code quality and maintainability.          |
| **UI/Styling** | [**Tailwind CSS**](https://tailwindcss.com/) + [**Shadcn/ui**](https://ui.shadcn.com/)                        | Rapidly build a modern, responsive, and accessible UI without leaving the HTML.              |
| **Backend & Database** | [**Supabase**](https://supabase.com/)                                                                       | The ultimate all-in-one BaaS: provides Postgres DB, Authentication, and Storage out-of-the-box, drastically cutting down on setup time. |
| **AI Integration** | [**OpenAI API (GPT-4o)**](https://openai.com/api/)                                                          | State-of-the-art model for reliable JSON generation (for quizzes) and quality explanations.  |
| **PDF Handling** | [**react-pdf**](https://github.com/wojtekmaj/react-pdf) (Frontend), [**pdf-parse**](https://www.npmjs.com/package/pdf-parse) (Backend) | Robust libraries for displaying and extracting text from PDF files.                           |
| **Deployment** | [**Vercel**](https://vercel.com/)                                                                           | Seamless, zero-config deployment for Next.js applications with automatic CI/CD.              |

---

## 🤖 The Development Journey: How LLMs Were Used

As per the assignment's instructions, LLMs (specifically Gemini and GitHub Copilot) were used aggressively as a pair-programming tool to accelerate development. Here’s how:

1.  **Project Planning & Architecture:**
    * Brainstormed the initial tech stack and database schema.
    * Generated the day-by-day action plan, including API contracts (request/response shapes) and component prop definitions.

2.  **Code Scaffolding & Boilerplate:**
    * Generated the initial code for Next.js API routes, including Supabase client setup and request handling.
    * Created the basic structure for React components (e.g., `Quiz.tsx`, `PDFUploader.tsx`) with TypeScript interfaces.

3.  **Core Logic Implementation:**
    * **Prompt Engineering:** Iteratively designed and refined the core LLM prompt for the quiz generation engine, focusing on forcing reliable JSON output and high-quality explanations.
    * **Complex Functions:** Wrote helper functions for tasks like score calculation and data transformation.

4.  **Database & SQL:**
    * Generated the initial `CREATE TABLE` SQL scripts for the Supabase database schema.
    * Wrote boilerplate for Supabase RLS (Row Level Security) policies to secure user data.

5.  **Documentation & Debugging:**
    * Generated this `README.md` file based on a structured outline.
    * Helped debug issues by providing context-aware suggestions and explaining potential error causes.

---

## 🏗️ System Architecture

The application follows a simple, scalable architecture:

1.  **Frontend (Next.js/React)**: The user interacts with the UI, which is rendered by Next.js on the server and client.
2.  **Backend (Next.js API Routes)**: The frontend communicates with our own backend API routes for actions like uploading files and generating quizzes.
3.  **Supabase**: Our backend API routes interact with Supabase for:
    * **Auth**: To manage user sessions.
    * **Storage**: To store uploaded PDF files.
    * **Database**: To persist user data, PDF metadata, and quiz attempts.
4.  **OpenAI API**: The `/api/generate-quiz` route sends the extracted PDF text to the OpenAI API and receives the structured quiz data back as JSON.

```
[User] <--> [Next.js Frontend] <--> [Next.js API Routes] <--> [OpenAI API]
                                         ^
                                         |
                                         v
                                    [Supabase (Auth, DB, Storage)]
```

---

## 🚀 Getting Started (Local Setup)

To get a local copy up and running, follow these simple steps.

### Prerequisites

-   Node.js (v18 or later)
-   npm or yarn
-   A Supabase account (free tier is sufficient)
-   An OpenAI API key

### Installation

1.  **Clone the repository**
    ```sh
    git clone [https://github.com/your-username/learn-lens.git](https://github.com/your-username/learn-lens.git)
    cd learn-lens
    ```

2.  **Install NPM packages**
    ```sh
    npm install
    ```

3.  **Set up environment variables**
    -   Create a file named `.env.local` in the root of your project.
    -   Copy the contents of `.env.local.example` into it.
    -   Fill in your Supabase Project URL, Anon Key, and your OpenAI API Key. You can find these in your Supabase and OpenAI dashboards.

    ```env
    # .env.local
    NEXT_PUBLIC_SUPABASE_URL="YOUR_SUPABASE_URL"
    NEXT_PUBLIC_SUPABASE_ANON_KEY="YOUR_SUPABASE_ANON_KEY"
    OPENAI_API_KEY="YOUR_OPENAI_API_KEY"
    ```

4.  **Run the development server**
    ```sh
    npm run dev
    ```

5.  Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

---

## 🤔 Tradeoffs & Decisions

Given the short timeframe, several strategic decisions were made:

-   **Backend-as-a-Service (BaaS) > Self-Hosted**: Chose Supabase over a custom Node.js/Express backend with a separate database to eliminate boilerplate and setup time for auth, storage, and database management.
-   **Component Library > Custom CSS**: Used Shadcn/ui to get a polished, professional look quickly, allowing more time to be spent on core application logic.
-   **Prioritizing Core Features**: Focused entirely on delivering the "Must-Have" features to a high standard rather than partially implementing all features. The Chat UI was deprioritized as it was a "Nice-to-Have".

---

## 🔮 Future Improvements

-   **Implement RAG for Chat**: Build the RAG pipeline using Supabase `pgvector` for highly accurate, cited answers.
-   **Improve Progress Tracking**: Add more granular analytics, such as performance by topic (by having the LLM tag questions).
-   **Caching**: Implement caching for generated quizzes to reduce redundant OpenAI API calls and lower costs.
-   **Batch Processing for PDFs**: For very large PDFs, text extraction and embedding should be handled as a background job to avoid timing out HTTP requests.
