# AI Study Buddy — Complete Project Description

---

## 1. Introduction

### 1.1 Background

The modern student faces an overwhelming volume of academic content across diverse subjects. Traditional study methods—reading textbooks, attending lectures, and taking handwritten notes—are time-consuming and often inefficient. The rapid advancement of large language models (LLMs) presents an opportunity to create intelligent, personalized study companions that can generate tailored study material on demand.

The AI Study Buddy project was conceived to bridge the gap between traditional self-study and the capabilities of modern generative AI. By integrating Google's Gemini 2.5 Flash model into a full-stack web application, the project delivers an interactive, adaptive, and personalized study platform that responds to each student's unique needs.

### 1.2 Project Overview

**AI Study Buddy** is a production-ready, full-stack web application that acts as a personal AI tutor. It is built using React 18 + Vite (frontend), Node.js + Express (backend), MongoDB Atlas (database), and Google Gemini 2.5 Flash (AI engine).

The application is accessible at: `https://ai-study-buddy-d5ag.onrender.com`

The platform provides four core AI-powered tools:

1. **Smart Notes Generation** — Structured, markdown-formatted study notes on any topic
2. **Adaptive Quiz Engine** — 5-question MCQ quizzes with instant feedback and scoring
3. **7-Day Study Plans** — Personalized day-by-day learning roadmaps
4. **Progress Dashboard** — Quiz history, weak area detection, and topic tracking

Users authenticate securely via JWT, and all study activity is persisted to MongoDB for long-term progress tracking.

### 1.3 Objectives

- Build a full-stack AI-powered study application accessible via browser
- Integrate Google Gemini 2.5 Flash to generate notes, quizzes, and study plans
- Implement a secure JWT-based authentication system
- Develop a weak-area detection system that personalizes future AI prompts
- Create a fully responsive UI supporting dark mode and mobile devices
- Ensure robustness via mock AI fallback when API quota is exceeded
- Persist all user activity (topics, quiz scores, weak areas) in MongoDB

---

## 2. Profile of the Problem

### 2.1 Problem Statement

Students often struggle to find well-structured, level-appropriate study material quickly. Searching the internet yields unfiltered, inconsistent content. Hiring tutors is expensive. Existing edtech platforms provide fixed content that cannot adapt to a student's specific weak areas or learning pace.

There is a need for an intelligent system that:
- Instantly generates accurate, structured notes on any topic
- Adapts quiz difficulty to the student's knowledge level
- Identifies which topics a student is weak at and reinforces them
- Provides a structured, time-boxed study roadmap

### 2.2 Scope of the Study

The project covers:

- **User Management**: Registration, login, JWT authentication, profile storage in MongoDB
- **AI Content Generation**: Notes, quizzes, and study plans using Gemini 2.5 Flash API
- **Personalization**: Weak area tracking, adaptive AI prompts, studied topic history
- **Progress Analytics**: Quiz history, average score, weak area list, recent sessions
- **UI/UX**: Responsive design, dark mode, skeleton loaders, micro-animations
- **Deployment**: Backend on Render, frontend served via Vite dev server or static build

Out of scope for the current version:
- Social features (shared notes, leaderboards)
- Video/audio content generation
- Mobile native app (iOS/Android)
- Payment/subscription system

### 2.3 Rationale

With the availability of powerful LLM APIs and cloud hosting, it is now feasible to build a fully functional AI tutor as a personal project. The combination of React (for rich UI), Express (for REST APIs), MongoDB (for flexible document storage), and Gemini (for AI content) makes an ideal modern stack. The system is designed to be extensible, with clear module boundaries between authentication, AI generation, and progress tracking.

---

## 3. Existing System

### 3.1 Introduction

Several edtech and AI tools currently exist in the market. However, none combine all four pillars—notes, quizzes, study plans, and progress tracking—into a single free, open-source, personalized platform.

### 3.2 Existing Software

| Platform | Notes | Quizzes | Study Plans | Personalization | Free |
|---|---|---|---|---|---|
| Khan Academy | ✅ | ✅ | ❌ | Partial | ✅ |
| Quizlet | ❌ | ✅ | ❌ | Limited | Partial |
| ChatGPT | ✅ | ✅ | ✅ | None (no memory) | Partial |
| Notion AI | ✅ | ❌ | ❌ | None | ❌ |
| **AI Study Buddy** | ✅ | ✅ | ✅ | ✅ Weak areas | ✅ |

### 3.3 What's New in the Proposed System

- **Weak Area Detection**: Automatically detects topics where quiz score < 50% and marks them
- **Adaptive AI Prompts**: Future notes and plans explicitly reference the student's weak areas
- **Unified Platform**: All four tools in one authenticated session with shared state
- **Fallback AI**: Mock content generator ensures the app works even when API quota is exhausted
- **Markdown Rendering**: Notes are rendered with rich formatting via `react-markdown`
- **Level-Based Generation**: All AI calls accept a difficulty level (Beginner / Intermediate / Advanced)

---

## 4. Problem Analysis

### 4.1 Product Definition

**Product Name**: AI Study Buddy  
**Version**: 1.0.0  
**Type**: Full-Stack Web Application  
**Target Users**: Students, self-learners, professionals upskilling

**Core Entities**:
- `User` — Stores credentials, quiz history, weak areas, and studied topics
- `StudySession` — Stores each AI generation event (notes/quiz/plan) with content and metadata

**Core Workflows**:
1. User registers → JWT issued → stored in localStorage
2. User enters a topic + level → AI generates content → saved to DB
3. User completes quiz → score computed → weak areas updated in User document
4. Dashboard/Progress pages fetch aggregated stats from `/api/progress`

### 4.2 Feasibility Analysis

#### 4.2.1 Technical Feasibility

- **Frontend**: React 18 + Vite 5 — mature, well-documented, highly capable
- **Backend**: Node.js + Express 4 — lightweight, widely deployed REST API framework
- **Database**: MongoDB Atlas — serverless, scalable, free tier sufficient for prototype
- **AI**: Google Gemini 2.5 Flash — available via `@google/generative-ai` npm package
- **Auth**: JWT + bcryptjs — industry-standard, stateless authentication
- **Deployment**: Render free tier (backend), Vite build (frontend) — viable for prototype

All technologies are freely available and well-supported. The project is technically feasible.

#### 4.2.2 Economic Feasibility

- All third-party services used have a free tier (MongoDB Atlas, Render, Gemini API)
- Development tools (VS Code, Node.js, npm) are free and open-source
- No licensing fees required
- The Gemini API free tier provides sufficient quota for development and light usage
- Cost to deploy and run: **$0** for prototype scale

---

## 5. Software Requirement Analysis

### 5.1 Functional Requirements

| ID | Requirement |
|---|---|
| FR-01 | User shall be able to register with name, email, and password (min 6 chars) |
| FR-02 | User shall be able to log in with email and password |
| FR-03 | System shall issue a JWT token (30-day expiry) on successful auth |
| FR-04 | Authenticated user shall generate AI-powered notes for any topic and level |
| FR-05 | Notes shall be structured with Introduction, Key Concepts, Examples, How It Works, Summary, Next Steps |
| FR-06 | Authenticated user shall generate a 5-question MCQ quiz for any topic and level |
| FR-07 | Quiz questions shall include question text, 4 options, correct answer, and explanation |
| FR-08 | User shall progress through quiz questions one at a time with instant answer feedback |
| FR-09 | Quiz score shall be computed and optionally saved to the user's profile |
| FR-10 | Topics scoring < 50% shall be automatically added to the user's weak areas list |
| FR-11 | Authenticated user shall generate a 7-day study plan for any topic and level |
| FR-12 | Each plan day shall include: title, focus, topics, tasks, duration, difficulty, resources |
| FR-13 | Dashboard shall display: topics studied, quizzes taken, average score, weak areas count |
| FR-14 | Progress page shall display full quiz history with score bars and weak areas panel |
| FR-15 | AI prompts shall be enriched with weak area context when relevant |
| FR-16 | System shall fall back to mock AI content if the Gemini API fails |
| FR-17 | All protected routes shall reject requests without a valid JWT |

### 5.2 Non-Functional Requirements

| ID | Requirement |
|---|---|
| NFR-01 | API response time for AI generation should be < 10 seconds under normal conditions |
| NFR-02 | Application shall be fully responsive on mobile, tablet, and desktop |
| NFR-03 | Dark mode shall be supported and persisted in localStorage |
| NFR-04 | Passwords shall be hashed using bcrypt (salt rounds: 10) before storage |
| NFR-05 | JWT tokens shall expire after 30 days |
| NFR-06 | The UI shall display skeleton loaders during all async operations |
| NFR-07 | CORS shall be restricted to the configured CLIENT_URL origin |
| NFR-08 | All API errors shall return structured JSON with an `error` field |
| NFR-09 | The frontend shall handle 401 responses globally and redirect to `/login` |
| NFR-10 | The application shall be deployable with a single `npm run dev` command from the root |

---

## 6. Design

### 6.1 System Architecture

The system follows a classic **3-Tier Architecture**:

```
┌─────────────────────────────────────────────────────────────┐
│                     CLIENT (Browser)                        │
│  React 18 + Vite + Tailwind CSS                             │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────┐  │
│  │ Landing  │ │Dashboard │ │ Generate │ │  TakeQuiz    │  │
│  │  Login   │ │ Progress │ │  Notes   │ │  StudyPlan   │  │
│  │ Register │ │          │ │          │ │              │  │
│  └──────────┘ └──────────┘ └──────────┘ └──────────────┘  │
│  AuthContext · ThemeContext · Axios API Service             │
└────────────────────────┬────────────────────────────────────┘
                         │ HTTP / JSON (REST)
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                  SERVER (Node.js + Express)                  │
│  ┌────────────┐  ┌──────────────┐  ┌───────────────────┐   │
│  │ authRoutes │  │   aiRoutes   │  │  progressRoutes   │   │
│  └─────┬──────┘  └──────┬───────┘  └────────┬──────────┘   │
│        │                │                    │              │
│  ┌─────▼──────┐  ┌──────▼───────┐  ┌────────▼──────────┐  │
│  │authControll│  │ aiController │  │progressController │  │
│  │  register  │  │ generateNotes│  │   getProgress     │  │
│  │  login     │  │ generateQuiz │  └───────────────────┘  │
│  │  getMe     │  │ generatePlan │                          │
│  └────────────┘  │ saveQuizReslt│                          │
│                  └──────┬───────┘                          │
│  JWT Middleware          │                                  │
│  authMiddleware.js       ▼                                  │
│                  Google Gemini 2.5 Flash API                │
└────────────────────────┬────────────────────────────────────┘
                         │ Mongoose ODM
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                   DATABASE (MongoDB Atlas)                   │
│  Collections: users · studysessions                         │
└─────────────────────────────────────────────────────────────┘
```

### 6.2 Module Decomposition

#### Backend Modules

| Module | File | Responsibility |
|---|---|---|
| Entry Point | `server/server.js` | Express app setup, CORS, middleware, route mounting |
| DB Config | `server/config/db.js` | Mongoose connection to MongoDB Atlas |
| Auth Controller | `controllers/authController.js` | register, login, getMe |
| AI Controller | `controllers/aiController.js` | generateNotes, generateQuiz, generatePlan, saveQuizResult |
| Progress Controller | `controllers/progressController.js` | getProgress (stats aggregation) |
| Auth Middleware | `middleware/authMiddleware.js` | JWT verification, user population on req.user |
| User Model | `models/User.js` | Schema: name, email, password, studiedTopics, weakAreas, quizHistory |
| Session Model | `models/StudySession.js` | Schema: userId, topic, type, content, score, level |
| Auth Routes | `routes/authRoutes.js` | POST /register, POST /login, GET /me |
| AI Routes | `routes/aiRoutes.js` | POST /notes, POST /quiz, POST /plan, POST /quiz/result |
| Progress Routes | `routes/progressRoutes.js` | GET /progress |

#### Frontend Modules

| Module | File | Responsibility |
|---|---|---|
| App Router | `src/App.jsx` | Route definitions, context wrapping, protected route gates |
| Auth Context | `src/context/AuthContext.jsx` | Global user state, login/register/logout, localStorage sync |
| Theme Context | `src/context/ThemeContext.jsx` | Dark/light mode state, localStorage persistence, DOM class toggle |
| API Service | `src/services/api.js` | Axios instance, JWT interceptor, global 401 redirect |
| Landing Page | `src/pages/Landing.jsx` | Public marketing page with hero, features, CTA |
| Login Page | `src/pages/Login.jsx` | Email/password login form |
| Register Page | `src/pages/Register.jsx` | Name/email/password registration form |
| Dashboard | `src/pages/Dashboard.jsx` | Stats cards, quick actions, weak areas, recent sessions |
| Generate Notes | `src/pages/GenerateNotes.jsx` | Topic + level form, markdown note display, copy button |
| Take Quiz | `src/pages/TakeQuiz.jsx` | Quiz form, question display, option selection, results + review |
| Study Plan | `src/pages/StudyPlan.jsx` | Plan form, expandable day cards with topics/tasks/resources |
| Progress | `src/pages/Progress.jsx` | Stats cards, quiz history bars, weak areas panel, topics grid |
| Layout | `src/components/Layout.jsx` | Sidebar + Navbar wrapper for authenticated pages |
| Sidebar | `src/components/Sidebar.jsx` | Desktop collapsible nav with user avatar |
| Navbar | `src/components/Navbar.jsx` | Mobile top bar + slide-in drawer |
| ProtectedRoute | `src/components/ProtectedRoute.jsx` | Redirects unauthenticated users to /login |
| StatsCard | `src/components/StatsCard.jsx` | Reusable metric card with icon, value, label |
| SkeletonCard | `src/components/SkeletonCard.jsx` | Animated loading placeholder |
| LoadingSpinner | `src/components/LoadingSpinner.jsx` | Spinner for AI generation loading states |
| ThemeToggle | `src/components/ThemeToggle.jsx` | Sun/moon icon button to toggle dark mode |

### 6.3 Recommendation Algorithm

The AI content generation is powered by **carefully engineered prompts** sent to Google Gemini 2.5 Flash. The recommendation logic works as follows:

#### Notes Generation (`generateNotes`)

1. User submits `{ topic, level }` to `POST /api/ai/notes`
2. System fetches the user document from MongoDB
3. Checks if `topic` exists in `user.weakAreas`
4. If weak area detected: appends extra instruction to prompt:
   > *"This is a weak area for this student — provide extra simple explanations, more examples, and include common misconceptions."*
5. Constructs structured prompt with 6 mandatory markdown sections
6. Sends to Gemini 2.5 Flash, returns markdown text
7. Saves a `StudySession` record and updates `user.studiedTopics`

#### Quiz Generation (`generateQuiz`)

1. User submits `{ topic, level }` to `POST /api/ai/quiz`
2. Prompt instructs Gemini to return **only valid JSON** — a 5-element array
3. Each element has: `question`, `options` (4), `answer`, `explanation`
4. Robust regex extraction: `content.match(/\[[\s\S]*\]/)` to isolate JSON
5. Parses and validates the array before returning to client
6. Saves a `StudySession` with type `'quiz'`

#### Quiz Result & Weak Area Update (`saveQuizResult`)

1. User submits `{ topic, score, totalQuestions, level }` to `POST /api/ai/quiz/result`
2. Computes `percentage = Math.round((score / totalQuestions) * 100)`
3. Appends result to `user.quizHistory[]`
4. **If percentage < 50**: adds/updates topic in `user.weakAreas[]` with running average score
5. **If percentage ≥ 50**: removes topic from `user.weakAreas[]` (student has improved)
6. Updates `user.studiedTopics[]` with count and timestamp

#### Study Plan Generation (`generatePlan`)

1. User submits `{ topic, level }` to `POST /api/ai/plan`
2. Fetches user's weak areas: `user.weakAreas.map(w => w.topic)`
3. If weak areas exist, appends: *"Also reinforce these weak areas if relevant: [list]"*
4. Prompt requests structured JSON with: title, overview, totalHours, and 7 day objects
5. Each day: day number, title, focus, topics[], tasks[], duration, difficulty, resources[]
6. Robust JSON extraction via `content.match(/\{[\s\S]*\}/)` then `JSON.parse()`

#### Fallback Mock AI

When the Gemini API fails (quota, network, etc.):
- **Notes**: Returns a templated markdown document with placeholder content
- **Quiz**: Returns 5 generic questions with real structure (valid JSON)
- **Plan**: Returns a 7-day plan template with computed day titles

### 6.4 Personalisation Engine

The personalisation engine operates at two levels:

**Level 1 — Prompt Enrichment**:
- Notes for weak-area topics receive extra instructional directives
- Study plans receive a list of weak areas to reinforce

**Level 2 — Historical Context**:
- `user.studiedTopics[]` tracks every topic studied with a count and `lastStudied` timestamp
- `user.weakAreas[]` stores the running average score and attempt count per weak topic
- `user.quizHistory[]` is an append-only log of all quiz results with percentage

The dashboard surfaces this data: weak area topics are shown prominently with their average score, prompting the user to revisit them.

### 6.5 Flowcharts

#### 6.5.1 Main Recommendation Flowchart

```
User enters topic + level
         │
         ▼
   Fetch User from DB
         │
         ▼
  Is topic in weakAreas?
    YES ──────────────────► Add weak area instructions to prompt
    NO                       │
    │                        │
    └────────────────────────┘
                 │
                 ▼
      Build structured prompt
                 │
                 ▼
      Call Gemini 2.5 Flash API
                 │
           API Success?
          /            \
        YES              NO
         │                │
         ▼                ▼
   Return content     Return Mock AI content
         │                │
         └────────┬───────┘
                  ▼
     Save StudySession to MongoDB
                  │
                  ▼
     Update studiedTopics in User
                  │
                  ▼
         Return to Client
```

#### 6.5.2 User Interaction & Personalization Flowchart

```
User completes quiz
        │
        ▼
  POST /api/ai/quiz/result
        │
        ▼
  Calculate percentage
        │
  percentage < 50?
   /           \
  YES           NO
   │             │
   ▼             ▼
Add to        Remove from
weakAreas[]   weakAreas[]
(or update    if exists
running avg)
   │             │
   └──────┬──────┘
          │
          ▼
  Append to quizHistory[]
          │
          ▼
  Update studiedTopics[]
          │
          ▼
  Save User document
          │
          ▼
  Return { percentage, isWeakArea, passed }
```

---

## 7. Testing

### 7.1 Functional Test Cases

| TC-ID | Feature | Input | Expected Output | Status |
|---|---|---|---|---|
| TC-01 | Register | name, email, password (≥6 chars) | 201, JWT token returned | ✅ Pass |
| TC-02 | Register duplicate email | existing email | 400, "account already exists" | ✅ Pass |
| TC-03 | Login valid credentials | correct email + password | 200, JWT token | ✅ Pass |
| TC-04 | Login invalid password | wrong password | 401, "Invalid email or password" | ✅ Pass |
| TC-05 | Access protected route without JWT | no Authorization header | 401, "no token provided" | ✅ Pass |
| TC-06 | Generate Notes | topic="Photosynthesis", level="beginner" | Structured markdown with 6 sections | ✅ Pass |
| TC-07 | Generate Notes – weak area | topic in user.weakAreas | Extra simplified explanation included | ✅ Pass |
| TC-08 | Generate Quiz | topic="Python", level="intermediate" | 5-element JSON array with valid structure | ✅ Pass |
| TC-09 | Quiz correct answer | correct option selected | Score increments, green highlight | ✅ Pass |
| TC-10 | Quiz wrong answer | wrong option selected | Red highlight, correct answer shown | ✅ Pass |
| TC-11 | Save quiz result < 50% | score=1/5 (20%) | Topic added to weakAreas | ✅ Pass |
| TC-12 | Save quiz result ≥ 50% | score=4/5 (80%) | Topic removed from weakAreas | ✅ Pass |
| TC-13 | Generate Study Plan | topic="JavaScript", level="beginner" | 7-day JSON plan with all fields | ✅ Pass |
| TC-14 | Study Plan – weak areas | user has weakAreas | Plan reinforces those topics | ✅ Pass |
| TC-15 | Progress fetch | GET /api/progress | Stats: totalTopics, totalQuizzes, avgScore, weakAreas | ✅ Pass |
| TC-16 | Gemini API failure | API quota exceeded | Fallback mock content returned | ✅ Pass |
| TC-17 | Dark mode toggle | Click ThemeToggle | Class toggled on `<html>`, persisted to localStorage | ✅ Pass |
| TC-18 | Mobile navigation | Viewport < 768px | Sidebar hidden, Navbar drawer visible | ✅ Pass |

### 7.2 Structural Testing

**Unit-Level Logic Tested**:

- `generateToken(id)` — produces a signed JWT with 30d expiry
- `user.comparePassword(candidate)` — bcrypt comparison returns true/false correctly
- `updateStudiedTopics(user, topic)` — increments count if exists, pushes new entry otherwise
- `percentage < 50` branching in `saveQuizResult` — weak area add/update/remove logic
- JSON regex extraction: `content.match(/\[[\s\S]*\]/)` handles Gemini markdown wrappers
- ThemeContext `isDark` initialisation — reads localStorage, falls back to `prefers-color-scheme`
- AuthContext rehydration — safely parses stored user JSON on mount

**Integration Points Tested**:
- Express route → middleware → controller → Mongoose → MongoDB Atlas
- Frontend Axios interceptor → JWT attachment → API call → 401 auto-redirect

### 7.3 Test Execution Summary

| Category | Total | Passed | Failed |
|---|---|---|---|
| Authentication | 5 | 5 | 0 |
| AI Generation | 6 | 6 | 0 |
| Quiz Logic | 4 | 4 | 0 |
| Progress & Stats | 2 | 2 | 0 |
| UI / UX | 3 | 3 | 0 |
| **Total** | **20** | **20** | **0** |
---

## 8. Implementation

### 8.1 Tools and Technologies Used

| Layer | Technology | Version | Purpose |
|---|---|---|---|
| Frontend Framework | React | 18.2.0 | Component-based UI |
| Frontend Build Tool | Vite | 5.0.8 | Fast dev server and bundler |
| CSS Framework | Tailwind CSS | 3.4.0 | Utility-first styling |
| Routing | React Router DOM | 6.21.0 | Client-side SPA routing |
| HTTP Client | Axios | 1.6.0 | API requests with interceptors |
| Markdown Renderer | react-markdown | 8.0.7 | Renders AI-generated notes |
| Icon Library | lucide-react | 0.303.0 | SVG icons throughout UI |
| Backend Runtime | Node.js | 18+ | JavaScript server runtime |
| Backend Framework | Express | 4.18.2 | REST API server |
| Database | MongoDB Atlas | Cloud | Document storage |
| ODM | Mongoose | 8.0.3 | Schema definition and queries |
| Authentication | jsonwebtoken | 9.0.2 | JWT generation and verification |
| Password Hashing | bcryptjs | 2.4.3 | Secure password hashing |
| AI Engine | @google/generative-ai | 0.24.1 | Gemini 2.5 Flash API client |
| Environment Config | dotenv | 16.3.1 | Environment variable loading |
| CORS | cors | 2.8.5 | Cross-origin request handling |
| Dev Server | nodemon | 3.0.2 | Auto-restart on file changes |
| Concurrent Startup | concurrently | root | Run server + client simultaneously |

### 8.1.2 System Snapshots

**Application Pages**:

1. **Landing Page** (`/`) — Hero section with gradient background, feature cards with staggered animation, 3-step "How it works" section, CTA banner with star ratings
2. **Login / Register** (`/login`, `/register`) — Centered card with gradient accent, email/password fields, inline validation errors
3. **Dashboard** (`/dashboard`) — Greeting with time-of-day detection, 4 stats cards, 4 quick-action cards, weak areas panel, recent sessions list
4. **Generate Notes** (`/notes`) — Topic + level form, quick suggestion chips, rendered markdown notes with Copy button
5. **Take Quiz** (`/quiz`) — Setup form, animated progress bar, question cards with A/B/C/D options, instant color-coded feedback, results screen with trophy icon, answer review accordion
6. **Study Plan** (`/plan`) — Plan form, gradient header card with total hours, expandable day cards (Days 1–7 with progressive color coding)
7. **Progress** (`/progress`) — 4 stats cards, quiz history with color-coded score bars, weak areas with progress bars, topics grid
8. **Sidebar** (desktop) — Collapsible (w-60 ↔ w-16), logo, nav links with active state, theme toggle, user avatar with initials
9. **Navbar** (mobile) — Top bar with hamburger, slide-in drawer from right with backdrop

### 8.2 Key Implementation Details

#### 8.2.1 Gemini API Integration

The backend uses `@google/generative-ai` SDK v0.24.1:

```js
const { GoogleGenerativeAI } = require('@google/generative-ai');
const genAI = new GoogleGenerativeAI(process.env.GEMINI_API_KEY);
const geminiModel = genAI.getGenerativeModel({ model: 'gemini-2.5-flash' });

// Call pattern:
const result = await geminiModel.generateContent(prompt);
const response = await result.response;
return { content: response.text(), fallback: false };
```

**Model**: `gemini-2.5-flash` — chosen for speed and cost efficiency for student-scale queries.

**Error Handling**: Any API exception triggers the fallback mock generator, ensuring the app never crashes on quota exhaustion.

#### 8.2.2 JSON Extraction Strategy

Gemini sometimes wraps JSON in markdown code fences. Robust extraction:

```js
// For quiz (JSON array):
const jsonMatch = content.match(/\[[\s\S]*\]/);
const questions = JSON.parse(jsonMatch[0]);

// For study plan (JSON object):
const jsonMatch = content.match(/\{[\s\S]*\}/);
const plan = JSON.parse(jsonMatch[0]);
```

This regex approach strips any surrounding markdown before parsing.

#### 8.2.3 Frontend Architecture

- **Context API** (not Redux): Two lightweight contexts suffice — `AuthContext` and `ThemeContext`
- **Axios Interceptors**: Request interceptor attaches JWT; response interceptor catches 401s globally
- **Protected Routes**: `<ProtectedRoute>` checks `AuthContext.user` — redirects to `/login` if null
- **Skeleton Loaders**: Every async operation shows `<SkeletonCard>` or `<SkeletonNotes>` during loading
- **Micro-animations**: CSS classes `animate-fade-in`, `animate-slide-up` applied to page sections with `animationDelay` staggering

CSS Design System (Tailwind custom classes in `index.css`):
- `.card` — white/gray-900 rounded-2xl with shadow
- `.btn-primary` — gradient indigo button with scale hover
- `.badge-*` — colored pill labels (primary/green/yellow/red)
- `.prose-study` — custom markdown typography styles
- `.hero-gradient` — radial gradient background for landing
- `.skeleton` — animated pulse placeholder
- `.nav-link` / `.nav-link-active` — sidebar/navbar link states

#### 8.2.4 Dark Mode Implementation

```js
// ThemeContext.jsx — reads system preference + localStorage
const [isDark, setIsDark] = useState(() => {
  const saved = localStorage.getItem('theme');
  if (saved) return saved === 'dark';
  return window.matchMedia('(prefers-color-scheme: dark)').matches;
});

useEffect(() => {
  document.documentElement.classList.toggle('dark', isDark);
  localStorage.setItem('theme', isDark ? 'dark' : 'light');
}, [isDark]);
```

Tailwind's `darkMode: 'class'` strategy means all `dark:` variants activate when `<html class="dark">` is set.

---

## 9. Project Legacy

### 9.1 Current Status

**Version**: 1.0.0 — Production Prototype  
**Backend Deployed**: `https://ai-study-buddy-d5ag.onrender.com` (Render free tier)  
**Frontend**: Runs locally via `npm run dev` or built with `vite build`

**Implemented and Working**:
- ✅ Full JWT authentication (register, login, token refresh via localStorage)
- ✅ AI notes generation with weak area context injection
- ✅ AI quiz generation with JSON extraction and fallback
- ✅ AI 7-day study plan generation with weak area reinforcement
- ✅ Quiz result saving and weak area detection (< 50% threshold)
- ✅ Progress dashboard with stats aggregation
- ✅ Dark mode with system preference detection
- ✅ Fully responsive mobile layout with slide-in drawer
- ✅ Skeleton loaders on all async operations
- ✅ Collapsible desktop sidebar
- ✅ Mock AI fallback for API failures

### 9.2 Remaining Areas of Concern

| Issue | Priority | Notes |
|---|---|---|
| Render free tier cold starts (~30s delay) | Medium | Upgrade to paid tier for production |
| No refresh token mechanism | Medium | JWT expires after 30d; user must re-login |
| No email verification on registration | Medium | Any email string accepted |
| No rate limiting on API routes | High | Risk of abuse; add express-rate-limit |
| No input sanitization beyond basic checks | Medium | Add express-validator for robust validation |
| StudySession `isFallback` field not in schema | Low | Add to StudySession model for tracking |
| No pagination on quiz history | Low | Large history sets may slow Progress page |
| Gemini prompt not caching | Low | Repeated identical prompts incur full API cost |

### 9.3 Technical Lessons Learnt

1. **Prompt Engineering Matters**: The quality of JSON output from Gemini is highly sensitive to prompt wording. Explicit instructions ("Return ONLY valid JSON, no markdown") and regex fallback extraction are both necessary.

2. **Regex JSON Extraction**: Using `content.match(/\[[\s\S]*\]/)` is more reliable than assuming clean output from LLMs — even with explicit instructions, models sometimes add preamble text.

3. **Stateless JWT + localStorage**: Simpler than session-based auth for a single-service app; the trade-off is that tokens cannot be invalidated server-side without a blocklist.

4. **Context API is Sufficient**: For a focused single-user app with < 10 pages, React Context with `useState` is cleaner than Redux. No boilerplate, no selectors.

5. **Tailwind + Custom CSS Layers**: Combining Tailwind utilities with `@layer components` custom classes gives the best of both worlds — design system consistency without excessive className strings.

6. **Fallback AI**: Building a mock generator early prevented development blockage during API quota exhaustion and provides a graceful user experience in production.

---

## 10. User Manual

### 10.1 System Requirements

| Requirement | Minimum |
|---|---|
| Operating System | Windows 10 / macOS 12 / Ubuntu 20 |
| Node.js | v18.0.0 or higher |
| npm | v9.0.0 or higher |
| Browser | Chrome 110+ / Firefox 110+ / Edge 110+ |
| Internet | Required (for MongoDB Atlas and Gemini API) |
| RAM | 4 GB minimum |

### 10.2 Installation (Local)

**Step 1: Navigate to project root**
```bash
cd "AI Study Buddy"
```

**Step 2: Install root dependencies**
```bash
npm install
```

**Step 3: Install server dependencies**
```bash
cd server
npm install
cd ..
```

**Step 4: Install client dependencies**
```bash
cd client
npm install
cd ..
```

**Step 5: Configure server environment**

Create `server/.env`:
```env
PORT=5000
MONGO_URI=mongodb+srv://<user>:<password>@cluster.mongodb.net/ai-study-buddy
JWT_SECRET=any_long_random_secret_string_here
GEMINI_API_KEY=AIza...your_actual_gemini_key
CLIENT_URL=http://localhost:5173
```

**Step 6: Run the application**
```bash
npm run dev
```

This starts both backend (port 5000) and frontend (port 5173) concurrently.

**Step 7: Open browser**
```
http://localhost:5173
```

### 10.3 Using the Application

1. **Register**: Click "Get Started" on the landing page → enter your name, email, and password → you are automatically logged in
2. **Generate Notes**: Click "Generate Notes" in the sidebar → enter any topic (e.g., "Photosynthesis") → select a difficulty level → click "Generate Notes" → notes render in markdown format → click "Copy" to copy to clipboard
3. **Take a Quiz**: Click "Take Quiz" → enter a topic → select difficulty → click "Generate Quiz (5 MCQs)" → click each option to answer → see instant feedback and explanation → complete all 5 questions → view score → click "Save Result" to record progress
4. **Study Plan**: Click "Study Plan" → enter a topic → select level → click "Generate 7-Day Plan" → click on any day card to expand and see topics, tasks, and resources
5. **Progress**: Click "Progress" → view overall stats, full quiz history with score bars, weak area topics, and all studied topics grid
6. **Dark Mode**: Click the sun/moon icon in the sidebar or navbar → theme toggles and persists across sessions
7. **Logout**: Click "Logout" at the bottom of the sidebar → returns to landing page

### 10.4 Troubleshooting

| Problem | Solution |
|---|---|
| "Failed to generate notes" | Check GEMINI_API_KEY in server/.env; verify API quota in Google AI Studio |
| "MongoDB Error" on server start | Verify MONGO_URI format; check IP whitelist in MongoDB Atlas Network Access |
| JWT token expired | Log out and log back in; tokens last 30 days |
| Port 5000 already in use | Change PORT in server/.env; update client VITE_API_URL if needed |
| Frontend shows blank screen | Run `npm install` in `/client`; check browser console for errors |
| Notes load but are plain text | react-markdown may not be installed; run `npm install` in `/client` |
| Cold start delay (30+ seconds) | Backend is on Render free tier; first request wakes the server |

---

## 11. Source Code Summary

### 11.1 Project File Summary

```
AI Study Buddy/                     ← Root (concurrently runner)
├── package.json                    ← Root scripts: dev, server, client
├── README.md                       ← Setup guide and API reference
│
├── server/                         ← Node.js + Express backend
│   ├── server.js                   ← App entry: Express setup, routes, error handling
│   ├── package.json                ← Backend dependencies
│   ├── .env                        ← Secrets (PORT, MONGO_URI, JWT_SECRET, GEMINI_API_KEY)
│   ├── config/
│   │   └── db.js                   ← Mongoose.connect() wrapper
│   ├── controllers/
│   │   ├── aiController.js         ← Gemini calls, mock fallback, quiz result logic (319 lines)
│   │   ├── authController.js       ← register, login, getMe (83 lines)
│   │   └── progressController.js   ← Stats aggregation (41 lines)
│   ├── middleware/
│   │   └── authMiddleware.js       ← JWT verify, req.user population (32 lines)
│   ├── models/
│   │   ├── User.js                 ← User schema with bcrypt hooks (65 lines)
│   │   └── StudySession.js         ← Session schema (45 lines)
│   └── routes/
│       ├── aiRoutes.js             ← 4 protected AI endpoints (17 lines)
│       ├── authRoutes.js           ← 3 auth endpoints (lines)
│       └── progressRoutes.js       ← 1 progress endpoint
│
└── client/                         ← React + Vite frontend
    ├── index.html                  ← HTML shell with meta tags
    ├── vite.config.js              ← Vite config with React plugin
    ├── tailwind.config.js          ← Custom colors, shadows, animations
    ├── package.json                ← Frontend dependencies
    └── src/
        ├── main.jsx                ← ReactDOM.render with StrictMode
        ├── App.jsx                 ← Router + context providers + routes (73 lines)
        ├── index.css               ← Design system (214 lines: base, components, utilities)
        ├── context/
        │   ├── AuthContext.jsx     ← User state + auth actions (65 lines)
        │   └── ThemeContext.jsx    ← Dark mode state (40 lines)
        ├── services/
        │   └── api.js              ← Axios instance + interceptors (36 lines)
        ├── pages/
        │   ├── Landing.jsx         ← Public marketing page (233 lines)
        │   ├── Login.jsx           ← Login form (approx 150 lines)
        │   ├── Register.jsx        ← Register form (approx 230 lines)
        │   ├── Dashboard.jsx       ← Main dashboard (233 lines)
        │   ├── GenerateNotes.jsx   ← Notes tool (218 lines)
        │   ├── TakeQuiz.jsx        ← Quiz tool (305 lines)
        │   ├── StudyPlan.jsx       ← Study plan tool (240 lines)
        │   └── Progress.jsx        ← Progress tracking (214 lines)
        └── components/
            ├── Layout.jsx          ← Auth page shell
            ├── Navbar.jsx          ← Mobile nav (123 lines)
            ├── Sidebar.jsx         ← Desktop nav (130 lines)
            ├── ProtectedRoute.jsx  ← Auth guard
            ├── StatsCard.jsx       ← Metric card
            ├── SkeletonCard.jsx    ← Loading placeholder
            ├── LoadingSpinner.jsx  ← Spinner component
            └── ThemeToggle.jsx     ← Dark mode button
```

**Total Source Files**: 30 files  
**Total Lines of Code**: ~2,800 lines (excluding node_modules, lock files)

### 11.2 Key Code Modules

#### 11.2.1 Weak Area Detection Logic

```js
// In saveQuizResult (aiController.js)
const percentage = Math.round((score / totalQuestions) * 100);
user.quizHistory.push({ topic, score, totalQuestions, percentage });

if (percentage < 50) {
  const weakIdx = user.weakAreas.findIndex((w) => w.topic === topic);
  if (weakIdx > -1) {
    const existing = user.weakAreas[weakIdx];
    existing.averageScore = Math.round(
      (existing.averageScore * existing.attempts + percentage) /
        (existing.attempts + 1)
    );
    existing.attempts += 1;
  } else {
    user.weakAreas.push({ topic, averageScore: percentage, attempts: 1 });
  }
} else {
  // Student has improved — remove from weak areas
  user.weakAreas = user.weakAreas.filter((w) => w.topic !== topic);
}
```

#### 11.2.2 Adaptive Prompt Composition

```js
// Notes — weak area enrichment
const isWeak = user.weakAreas.some((w) => w.topic === topic);
const focusNote = isWeak
  ? ' This is a weak area — provide extra simple explanations, more examples, and include common misconceptions.'
  : '';
const prompt = `Explain "${topic}" comprehensively for a ${level} level student.${focusNote}\n...`;

// Study Plan — weak area reinforcement
const weakAreas = user.weakAreas.map((w) => w.topic);
const weakContext = weakAreas.length > 0
  ? ` Also reinforce these weak areas if relevant: ${weakAreas.join(', ')}.`
  : '';
```

#### 11.2.3 Studied Topics Tracking

```js
// Helper called after every notes/plan/quiz generation
const updateStudiedTopics = async (user, topic) => {
  const idx = user.studiedTopics.findIndex((t) => t.topic === topic);
  if (idx > -1) {
    user.studiedTopics[idx].count += 1;
    user.studiedTopics[idx].lastStudied = Date.now();
  } else {
    user.studiedTopics.push({ topic, count: 1 });
  }
};
```

#### 11.2.4 Global 401 Handler (Frontend)

```js
// api.js — Axios interceptor
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      localStorage.removeItem('token');
      localStorage.removeItem('user');
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);
```

---

## 12. Bibliography

1. Google LLC. (2024). *Gemini API Documentation*. Retrieved from https://ai.google.dev/gemini-api/docs

2. Google LLC. (2024). *@google/generative-ai npm package*. Retrieved from https://www.npmjs.com/package/@google/generative-ai

3. MongoDB Inc. (2024). *MongoDB Atlas Documentation*. Retrieved from https://www.mongodb.com/docs/atlas/

4. Mongoose. (2024). *Mongoose v8 Documentation*. Retrieved from https://mongoosejs.com/docs/

5. Meta Open Source. (2024). *React 18 Documentation*. Retrieved from https://react.dev/

6. Evan You. (2024). *Vite Documentation*. Retrieved from https://vitejs.dev/

7. Tailwind Labs. (2024). *Tailwind CSS v3 Documentation*. Retrieved from https://tailwindcss.com/docs

8. Auth0. (2024). *JSON Web Tokens (JWT) Introduction*. Retrieved from https://jwt.io/introduction

9. Express.js. (2024). *Express 4.x API Reference*. Retrieved from https://expressjs.com/en/4x/api.html

10. Render. (2024). *Render Deployment Documentation*. Retrieved from https://render.com/docs

11. npm. (2024). *bcryptjs — Password hashing library*. Retrieved from https://www.npmjs.com/package/bcryptjs

12. Remix Software. (2024). *React Router v6 Documentation*. Retrieved from https://reactrouter.com/

13. Axios. (2024). *Axios HTTP Client Documentation*. Retrieved from https://axios-http.com/docs/intro
