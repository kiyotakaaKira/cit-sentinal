# 🛡️ CIT-Sentinel — AI-Powered Academic Intelligence Platform

> **Predict dropout before it happens. Intervene before it's too late.**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-cit--sentinal.vercel.app-blue?style=for-the-badge)](https://cit-sentinal.vercel.app)
[![GitHub](https://img.shields.io/badge/GitHub-kiyotakaaKira%2Fcit--sentinal-black?style=for-the-badge&logo=github)](https://github.com/kiyotakaaKira/cit-sentinal)
[![SDG 4](https://img.shields.io/badge/SDG%204-Quality%20Education-red?style=for-the-badge)](https://sdgs.un.org/goals/goal4)
[![MongoDB Atlas](https://img.shields.io/badge/MongoDB-Atlas-green?style=for-the-badge&logo=mongodb)](https://www.mongodb.com/atlas)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Solution](#solution)
- [Sentinel Score Formula](#sentinel-score-formula)
- [Features](#features)
- [Role-Based Dashboards](#role-based-dashboards)
- [Novelty Features](#novelty-features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [Installation & Setup](#installation--setup)
- [Environment Variables](#environment-variables)
- [Database](#database)
- [API Reference](#api-reference)
- [Demo Credentials](#demo-credentials)
- [Real-Time System](#real-time-system)
- [AI Integration](#ai-integration)
- [Email System](#email-system)
- [SDG 4 Alignment](#sdg-4-alignment)
- [Deployment](#deployment)
- [Team](#team)

---

## 🌟 Overview

**CIT-Sentinel** is an AI-driven student retention and dropout prevention platform built for **Chennai Institute of Technology**. It monitors every student across five academic dimensions in real time, assigns a predictive **Sentinel Score**, classifies their behavioural risk pattern, and triggers structured multi-role interventions — all before performance decline becomes irreversible.

Built for the hackathon track aligned with **UN Sustainable Development Goal 4: Quality Education**.

---

## 🔴 Problem Statement

Indian engineering colleges usually lose 8–12% of students to dropout every academic year. The core failure is not a lack of care — it is a lack of **visibility** and **timing**.

| Problem | Impact |
|---|---|
| Faculty detect failure only after exams | Intervention comes too late |
| No unified view of attendance + marks + behaviour | Fragmented data, no risk picture |
| Mentors manage 20+ students manually | No scalable early warning |
| HODs receive monthly Excel reports | Zero real-time oversight |
| Students have no self-reporting channel | Wellbeing signals are invisible |
| No cross-role intervention pipeline | Actions don't link across hierarchy |

**Result:** Students fail in silence. Colleges react instead of preventing.

---

## ✅ Solution

CIT-Sentinel solves this with a **5-layer intervention architecture**:

```
DETECT → CLASSIFY → ALERT → INTERVENE → TRACK
```

1. **DETECT** — Sentinel Score calculated from 5 data dimensions every time Data changes  
2. **CLASSIFY** — Behavioural Persona Engine labels why a student is at risk
3. **ALERT** — Role-based notifications + real parent email alerts via Nodemailer
4. **INTERVENE** — AI generates 4-week intervention plans; peer bridge matching activates
5. **TRACK** — MongoDB Atlas stores every action; Activity Log provides full audit trail

---

## 🧮 Sentinel Score Formula

Every student receives a score from 0–100, recalculated automatically on every data change via a Mongoose pre-save hook:

```
Sentinel Score =
  (Attendance / 100)          × 30  pts  [max 30]
  (IAT1 + IAT2) / 100)        × 25  pts  [max 25]
  (LMS Activity / 100)        × 20  pts  [max 20]
  (Model Exam / 100)          × 15  pts  [max 15]
  min(Hackathon Wins × 5, 10)           [max 10]
                                ─────────────────
                                TOTAL   [max 100]
```

### Risk Classification

| Score Range | Status | Color | Action |
|---|---|---|---|
| 75 – 100 | ✅ Safe | Green | Monitor |
| 50 – 74 | ⚠️ At-Risk | Orange | Mentor intervention |
| 40 – 49 | 🔵 Observation | Blue | Teacher alert |
| 0 – 39 | 🔴 Critical | Red | Emergency protocol |

---

## 🚀 Features

### Core Platform Features

- **Live Sentinel Score** — auto-recalculates on every mark entry or attendance update
- **Behavioural Persona Engine** — classifies 8 risk patterns with tailored intervention strategies
- **Role-Based Access Control** — 6 distinct dashboards, JWT-authenticated
- **Real-Time Data Sync** — Server-Sent Events broadcast changes to all connected dashboards
- **Cross-Dashboard Intervention Pipeline** — actions in one role reflect in another within 15 seconds
- **MongoDB Atlas Integration** — all data persisted in cloud, Mumbai region (ap-south-1)
- **Automated Email Alerts** — Nodemailer sends real emails for parent alerts, escalations, meetings
- **Activity Audit Log** — every data change recorded with who, what, when
- **560+ Student Dataset** — synthetic students across 4 departments with realistic risk distribution

### Novelty Features

- **Dropout Oracle AI** — structured LLM analysis per student, not a chatbot
- **What-If Simulator** — project impact of interventions before applying them
- **Peer Bridge Smart Matcher** — algorithm-based peer mentor matching
- **Student Self-Report System** — anonymous weekly wellbeing check-ins
- **Predictive Risk Timeline** — week-by-week dropout projection with/without Sentinel
- **Student DNA Card** — full radar chart + intervention history + action panel per student
- **Live Score Breakdown** — animated bar showing exactly how each point was earned
- **Institution Scorecard** — A/B/C graded report card for Chairman view
- **Inline Mark Editing** — double-click any cell to edit, Enter to save to MongoDB

---

## 👥 Role-Based Dashboards

### 🎓 Student Dashboard
- Personal Sentinel Score ring with animated breakdown
- My Progress: weekly attendance chart, IAT bar chart, drift analysis
- Ask Sentinel AI: personal AI coach powered by Llama/Claude
- Concept Videos: curated real YouTube links for syllabus topics
- Weekly Goals checklist with progress tracking
- Self-Report: anonymous mood + confidence check-in

### 📖 Subject Teacher Dashboard
- Class Overview: full table of all students with real-time data
- At-Risk Students: filtered view of Critical + At-Risk only
- Mark Entry: live student search, form submission saves to MongoDB + recalculates scores
- Reports: downloadable CSV and Excel exports

### 🧑‍🏫 Mentor Dashboard
- Mentee Dashboard: card grid with risk badges
- Student Management: full CRUD — Add, Edit, Delete students with live score preview
- Intervention Plans: AI-generated 4-week plans saved to MongoDB + emailed to student
- Peer Bridge: smart matcher algorithm + bridge activation + weekly check-in tracking
- Schedule Meeting: date/time picker, saves to DB, sends confirmation email
- Parent Alert: saves to DB + sends real email via Nodemailer
- Dropout Oracle AI: per-student structured AI analysis

### 🏛️ HOD Dashboard
- Department Overview: 6 KPI cards fed from live MongoDB aggregation
- Risk Analytics: weekly trend chart, pattern breakdown
- Risk Timeline: predictive dual-line chart showing Sentinel impact
- What-If Simulator: sliders projecting score changes across population
- Dropout Insights AI: cause analysis with deep-dive per category
- Intervention Audit: table of all interventions with filter by status
- Activity Log: full audit trail of all data changes in department
- Student Editor: right-side drawer for quick field edits

### 🏫 Principal Dashboard
- Institution Overview: cross-department KPI cards
- Escalation Panel: live-loaded from MongoDB, with Acknowledge + Resolve actions
- Compliance Tracker: department-wise attendance compliance bars
- All escalations trigger automatic email to Principal on creation

### 👑 Chairman Dashboard
- Strategic Dashboard: Radar chart + weekly risk trend + KPI strip
- Industry Readiness: scatter plot of top performers
- SDG 4 Impact: dropout projection area chart + impact metrics
- Institution Scorecard: A/B/C graded scorecard with benchmark comparison
- Institution Report: auto-generated text report with Print + Copy

---

## 🔬 Novelty Features

### 1. Behavioural Persona Engine
Eight distinct risk personas, each with specific intervention strategy:

| Persona | Signal | Strategy |
|---|---|---|
| Technical Star | High hackathon wins, low IAT | Engage via strengths, not warnings |
| Lab Drift | Theory present, lab absent | Check timetable clashes first |
| Cramming Pattern | High LMS, low scores | Shift to active recall techniques |
| Burnout Pattern | Former high performer, sudden drop | Emotional check-in before academics |
| Theory Drift | Good scores, poor attendance | Flexible engagement plan |
| Full Dropout | Multi-dimensional failure | Emergency: parent + counselor |
| Steady Performer | Consistent, low risk | Candidate for peer mentor role |
| Top Performer | Exceeds all benchmarks | Nominate for competition representation |

### 2. What-If Simulator
Mentors and HODs adjust sliders to project intervention impact:
- Attendance Boost (+0% to +20%)
- Late Submission Reduction (0 to -8)
- LMS Engagement Boost (+0% to +50%)
- Peer Bridge Activation (0 to 20 pairs)
- Mentor Meeting Frequency (0 to 4/month)

Output: Projected Safe count, Projected Critical count, Dropouts Prevented

### 3. Peer Bridge Smart Matcher
```javascript
// Compatibility scoring algorithm
score =
  (same department)    ? +30 : 0
  (same year)          ? +20 : 0
  (sentinelScore > 75) ? +25 : 0
  (hackathonWins > 0)  ? +15 : 0
  (lateSubmissions = 0)? +10 : 0
```

### 4. Dropout Oracle AI
Structured prompt engineering — not a generic chatbot:
- Inputs: student's full data object (attendance, scores, persona, trend)
- Output: structured JSON with risk probability, 3 root causes, 4-week plan
- Model: Llama 3.2 (local Ollama) with Claude Sonnet fallback

### 5. Student Self-Report System
- 5-question emoji-rated weekly check-in (mood, IAT confidence, challenges, syllabus understanding, mentor support)
- Optional anonymous free-text note
- Mentor sees anonymised summary only — never individual identity
- Alerts if any student scores ≤ 2 on any dimension

---

## 🛠️ Tech Stack

### Frontend
| Technology | Version | Purpose |
|---|---|---|
| React | 18 | UI framework |
| Vite | Latest | Build tool + dev server |
| TypeScript | 5 | Type safety |
| Tailwind CSS | 3 | Utility-first styling |
| shadcn/ui | Latest | Component library |
| Recharts | Latest | All charts |
| Sonner | Latest | Toast notifications |
| Lucide React | Latest | Icons |

### Backend
| Technology | Version | Purpose |
|---|---|---|
| Node.js | 17+ | Runtime |
| Express | 4 | REST API server |
| Mongoose | 7 | MongoDB ODM |
| JWT | Latest | Authentication |
| bcryptjs | Latest | Password hashing |
| Nodemailer | Latest | Email delivery |
| Nodemon | Latest | Dev auto-restart |

### Database & Cloud
| Service | Purpose |
|---|---|
| MongoDB Atlas | Primary database (AWS ap-south-1) |
| Vercel | Frontend deployment |

### AI
| Model | Purpose |
|---|---|
| Llama 3.2 (Ollama) | Local AI inference — primary |
| Claude Sonnet (Anthropic API) | Cloud AI fallback |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────┐
│                   FRONTEND (Vite :8080)              │
│  React + TypeScript + Tailwind + shadcn/ui           │
│  6 Role Dashboards + DataContext (global state)      │
│  Server-Sent Events listener (real-time updates)     │
└──────────────────────┬──────────────────────────────┘
                       │ HTTP + JWT
                       │ Proxy: /api → :3001
┌──────────────────────▼──────────────────────────────┐
│                BACKEND (Express :3001)               │
│  REST API + SSE broadcast                            │
│  JWT Auth middleware                                 │
│  Role-based route protection                         │
│  Nodemailer email system                             │
│  Activity logging on every mutation                  │
└──────┬───────────────────────────────┬──────────────┘
       │ Mongoose ODM                  │ fetch
┌──────▼──────────┐          ┌─────────▼──────────────┐
│  MongoDB Atlas  │          │  AI Inference           │
│  5 Collections  │          │  Ollama :11434          │
│  AWS Mumbai     │          │  Llama 3.2 / sentinel-ai│
│                 │          │  Claude API (fallback)   │
└─────────────────┘          └────────────────────────┘
```

### MongoDB Collections

| Collection | Purpose | Key Fields |
|---|---|---|
| `students` | All student records | id, name, dept, year, scores, sentinelScore, status, persona |
| `interventions` | All intervention actions | studentId, type, status, createdBy, priority |
| `markentries` | Individual mark records | studentId, testType, score, maxScore, percentage |
| `peerbridges` | Peer mentor assignments | atRiskStudentId, mentorStudentId, compatibilityScore |
| `selfreports` | Student wellbeing check-ins | studentId, week, mood scores, challenges |
| `activitylogs` | Full audit trail | action, performedBy, targetId, previousValue, newValue |
| `users` | Authentication records | userId, password, role, department |

---

## 📁 Project Structure

```
cit-aura-dash-main/
├── src/
│   ├── components/
│   │   ├── views/
│   │   │   ├── StudentView.tsx
│   │   │   ├── TeacherView.tsx
│   │   │   ├── MentorView.tsx
│   │   │   ├── HODView.tsx
│   │   │   ├── PrincipalView.tsx
│   │   │   └── ChairmanView.tsx
│   │   ├── novel/
│   │   │   ├── StudentDNACard.tsx
│   │   │   ├── RiskTimeline.tsx
│   │   │   ├── PeerBridgeMatcher.tsx
│   │   │   ├── StudentSelfReport.tsx
│   │   │   ├── InstitutionScorecard.tsx
│   │   │   └── StudentMarksTable.tsx
│   │   ├── ui/                    (shadcn components)
│   │   ├── DashboardLayout.tsx
│   │   ├── LoginPage.tsx
│   │   └── ErrorBoundary.tsx
│   ├── context/
│   │   ├── AuthContext.tsx        (JWT auth + fallback)
│   │   └── DataContext.tsx        (global state + sync)
│   ├── hooks/
│   │   ├── useStudents.ts         (real-time student data)
│   │   ├── useDashboardStats.ts   (live KPI aggregation)
│   │   ├── useMarks.ts            (mark entry operations)
│   │   └── useRealtimeUpdates.ts  (SSE stream listener)
│   ├── utils/
│   │   ├── api.ts                 (all API call functions)
│   │   └── claudeAI.ts            (AI integration)
│   ├── data/
│   │   └── students.ts            (fallback local data)
│   └── main.tsx
├── backend/
│   ├── models/
│   │   ├── Student.js             (schema + pre-save hook)
│   │   ├── User.js
│   │   ├── Intervention.js
│   │   ├── MarkEntry.js
│   │   ├── PeerBridge.js
│   │   ├── SelfReport.js
│   │   └── ActivityLog.js
│   ├── utils/
│   │   └── mailer.js              (Nodemailer email templates)
│   ├── server.js                  (all routes + SSE)
│   ├── seed.js                    (user seed)
│   ├── seedStudents.js            (560 student seed)
│   ├── Modelfile                  (Ollama custom model)
│   ├── package.json
│   └── .env
├── vite.config.ts                 (proxy :8080 → :3001)
├── package.json
└── .env
```

---

## ⚙️ Installation & Setup

### Prerequisites

- Node.js v17 or higher
- npm v8 or higher
- MongoDB Atlas account (free tier works)
- Ollama installed (optional, for local AI)
- Gmail account with App Password (for email)

### Step 1 — Clone the Repository

```bash
git clone https://github.com/kiyotakaaKira/cit-sentinal.git
cd cit-aura-dash-main
```

### Step 2 — Install Frontend Dependencies

```bash
npm install
```

### Step 3 — Install Backend Dependencies

```bash
cd backend
npm install
```

### Step 4 — Configure Environment Variables

Create `backend/.env`:
```env
PORT=3001
MONGODB_URI=mongodb+srv://citadmin:CITSentinel2025@cit-sentinel.xxxxx.mongodb.net/cit-sentinel
JWT_SECRET=cit-sentinel-secret-key-2025
EMAIL_USER=your_gmail@gmail.com
EMAIL_PASS=your_16_char_app_password
PRINCIPAL_EMAIL=principal@citchennai.net
NODE_ENV=development
```

Create `.env` in root:
```env
VITE_API_URL=http://localhost:3001
VITE_ANTHROPIC_API_KEY=your_claude_api_key_optional
```

### Step 5 — Seed the Database

```bash
# Seed authentication users (8 role accounts)
cd backend
node seed.js

# Seed 560 synthetic students across 4 departments
node seedStudents.js
```

Expected output:
```
✅ SEEDING COMPLETE
...
```

> **Verification:** Open your MongoDB Atlas cluster after seeding and confirm that the `students`, `users`, `interventions`, and other project collections have been created successfully before starting the application.
==================
Total Students: 560

AI & DS:  130 students | Safe: 91 | At-Risk: 26 | Critical: 4
CSE:      170 students | Safe: 119 | At-Risk: 34 | Critical: 5
ECE:      150 students | Safe: 105 | At-Risk: 30 | Critical: 5
Mechanical: 110 students | Safe: 77 | At-Risk: 22 | Critical: 3
```

### Step 6 — Setup Ollama (Optional)

```bash
# Install Ollama from https://ollama.com
ollama pull llama3.2

# Create custom Sentinel AI model
cd backend
ollama create sentinel-ai -f Modelfile
```

### Step 7 — Run the Application

**Terminal 1 — Backend:**
```bash
cd backend
npm run dev
# Should show: ✅ CIT-Sentinel Backend running on port 3001
```

**Terminal 2 — Frontend:**
```bash
# From project root
npm run dev
# Should show: Local: http://localhost:8080
```

Open `http://localhost:8080`

### Port Conflict Fix

If you see `EADDRINUSE :::3001`:
```bash
# Windows
netstat -ano | findstr :3001
taskkill /PID <pid_number> /F

# Mac/Linux
lsof -ti:3001 | xargs kill -9
```

---

## 🔐 Environment Variables

### Backend (`backend/.env`)

| Variable | Required | Description |
|---|---|---|
| `PORT` | Yes | Backend server port (use 3001) |
| `MONGODB_URI` | Yes | MongoDB Atlas connection string |
| `JWT_SECRET` | Yes | JWT signing secret |
| `EMAIL_USER` | Yes | Gmail address for sending alerts |
| `EMAIL_PASS` | Yes | Gmail App Password (16 chars) |
| `PRINCIPAL_EMAIL` | No | Where escalation emails go |
| `NODE_ENV` | No | development / production |

### Frontend (`.env`)

| Variable | Required | Description |
|---|---|---|
| `VITE_API_URL` | Yes | Backend URL (http://localhost:3001) |
| `VITE_ANTHROPIC_API_KEY` | No | Claude API key for cloud AI fallback |

### Getting Gmail App Password

1. Go to [myaccount.google.com](https://myaccount.google.com)
2. Security → 2-Step Verification → Enable
3. Search "App Passwords"
4. Select: App = Mail, Device = Windows
5. Copy the 16-character password → paste as `EMAIL_PASS`

---

## 🗄️ Database

### Connection

MongoDB Atlas cluster: `cit-sentinel` on AWS Mumbai (ap-south-1)

```
Host: cit-sentinel.xxxxx.mongodb.net
Database: cit-sentinel
User: citadmin
IP Whitelist: 0.0.0.0/0 (all IPs)
```

### Student Data Distribution (560 students)

| Department | Year 1 | Year 2 | Year 3 | Year 4 | Total |
|---|---|---|---|---|---|
| AI & DS | 35 | 35 | 30 | 30 | 130 |
| CSE | 45 | 45 | 40 | 40 | 170 |
| ECE | 40 | 40 | 35 | 35 | 150 |
| Mechanical | 30 | 30 | 25 | 25 | 110 |
| **Total** | **150** | **150** | **130** | **130** | **560** |

### Risk Distribution

| Status | % of Students | Target |
|---|---|---|
| Safe | ~70% | ~392 |
| At-Risk | ~20% | ~112 |
| Observation | ~7% | ~39 |
| Critical | ~3% | ~17 |

### Sentinel Score Auto-Calculation

The `Student` model has a `pre('save')` hook that recalculates the Sentinel Score and Status automatically every time a student record is saved — no manual calculation needed anywhere in the codebase.

---

## 📡 API Reference

### Authentication

```
POST   /api/auth/login          Login and receive JWT
GET    /api/auth/verify         Verify existing token
```

### Students

```
GET    /api/students            Get all students (with filters)
GET    /api/students/:id        Get single student
POST   /api/students            Create new student (Mentor/HOD+)
PUT    /api/students/:id        Full update student
PATCH  /api/students/:id        Partial update student
DELETE /api/students/:id        Remove student (HOD+)
PATCH  /api/students/bulk/update  Bulk update multiple students
GET    /api/students/stats/department    Department aggregation
GET    /api/students/stats/institution  Institution-wide stats
```

### Marks

```
GET    /api/marks               Get mark entries (filterable)
POST   /api/marks               Add mark entry + auto-update student
PUT    /api/marks/:id           Update existing mark
DELETE /api/marks/:id           Remove mark entry
```

### Interventions

```
GET    /api/interventions       Get all interventions
POST   /api/interventions       Create intervention
PUT    /api/interventions/:id   Update intervention
DELETE /api/interventions/:id   Delete intervention
POST   /api/interventions/send-plan   Save plan + send email
```

### Escalations

```
GET    /api/escalations               Get all escalations
POST   /api/escalations               Create + email principal
PATCH  /api/escalations/:id/acknowledge   Acknowledge
PATCH  /api/escalations/:id/resolve       Resolve
```

### Peer Bridges

```
GET    /api/peer-bridges              Get active bridges
POST   /api/peer-bridges              Create new bridge
PATCH  /api/peer-bridges/:id/checkin  Log weekly check-in
```

### Alerts & Meetings

```
POST   /api/alerts/parent       Send parent alert + email
POST   /api/meetings            Schedule meeting + send email
```

### Self Reports

```
POST   /api/self-reports        Submit weekly check-in
GET    /api/self-reports/summary  Get anonymised summary
```

### Dashboard

```
GET    /api/dashboard/realtime  Live stats for current user's role
GET    /api/activity-log        Full audit trail (HOD+)
GET    /api/admin/collections-summary  MongoDB collection counts
GET    /api/notifications       Role-based notifications
```

### AI

```
POST   /api/ai/chat             Chat with Sentinel AI
POST   /api/ai/dropout-analysis Structured dropout analysis
```

### Real-Time

```
GET    /api/realtime/stream     Server-Sent Events stream
```

### Reports

```
POST   /api/reports/generate    Generate report record
```

### Query Parameters (GET /api/students)

```
?department=AI & DS     Filter by department
?year=2                 Filter by year
?status=Critical        Filter by risk status
?search=Arun            Search name or register number
```

---

## 🔑 Demo Credentials

| Role | User ID | Password | Access Level |
|---|---|---|---|
| Student | `CIT2022001` | `student123` | Own data only |
| Student | `CIT2022002` | `student456` | Own data only |
| Student | `CIT2022003` | `student789` | Own data only |
| Subject Teacher | `FAC001` | `teacher123` | Department students |
| Mentor | `MNT001` | `mentor123` | Department + CRUD |
| HOD | `HOD001` | `hod123` | Department + escalation |
| Principal | `PRN001` | `principal123` | All departments |
| Chairman | `CHR001` | `chairman123` | Full institution view |

> **Note:** If backend is offline, fallback credentials are hardcoded in `AuthContext.tsx` so the demo always works.

---

## ⚡ Real-Time System

CIT-Sentinel uses **Server-Sent Events (SSE)** for real-time cross-dashboard updates.

### How It Works

```
Teacher enters mark
       ↓
POST /api/marks → saves to MongoDB
       ↓
Student.save() → pre-save hook recalculates Sentinel Score
       ↓
broadcastUpdate('STUDENT_UPDATED', { id, name, score, status })
       ↓
All connected SSE clients receive the event
       ↓
MentorView, HODView, PrincipalView update their local state
       ↓
UI updates without any page refresh
```

### Events Broadcast

| Event Type | Trigger | Receivers |
|---|---|---|
| `STUDENT_UPDATED` | Any student field change | Mentor, HOD, Principal, Chairman |
| `INTERVENTION_ADDED` | New intervention saved | HOD, Principal |
| `MARK_ENTERED` | Teacher submits mark | Mentor (same dept) |
| `ESCALATION_CREATED` | HOD escalates student | Principal, Chairman |

### Polling Fallback

All hooks also poll MongoDB every 15–30 seconds as a fallback if SSE disconnects.

---

## 🤖 AI Integration

### Primary — Llama 3.2 (Local Ollama)

```
Endpoint: http://localhost:11434/api/chat
Model: sentinel-ai (custom Modelfile) or llama3.2
Context: Student data + role-specific system prompt
```

### Fallback — Claude Sonnet (Anthropic API)

```
Endpoint: https://api.anthropic.com/v1/messages
Model: claude-sonnet-4-20250514
Triggered: When Ollama is unavailable
```

### Dropout Oracle Analysis Flow

```javascript
// Input to AI
{
  student: { name, dept, year, attendance, iat1, iat2, model, lmsActivity, persona },
  role: "Mentor",
  request: "structured_dropout_analysis"
}

// Output from AI (JSON)
{
  riskProbability: 0.73,
  rootCauses: ["Low lab attendance", "Missing IAT 2", "High late submissions"],
  weeklyPlan: {
    week1: "Daily attendance check-in with mentor",
    week2: "Complete 3 missed LMS modules",
    week3: "Revise IAT 1 topics — scheduled slot",
    week4: "Mock IAT session with peer mentor"
  },
  recommendedPersona: "Lab Drift",
  urgency: "High"
}
```

### AI Prompt Strategy

Each role gets a different system prompt tone:
- **Student:** Warm, encouraging, coaching voice
- **Mentor:** Tactical, actionable, plan-focused
- **HOD:** Strategic, data-driven, pattern-focused
- **Chairman:** Executive summary, institution-level insights

---

## 📧 Email System

All emails sent via Nodemailer using Gmail App Password.

### Email Templates

| Trigger | Recipient | Subject |
|---|---|---|
| Parent Alert | Parent email | `⚠️ CIT-Sentinel Alert: [Student] Needs Attention` |
| Escalation | Principal | `🚨 Escalation: [Student] — Immediate Action Required` |
| Intervention Plan | Student | `📋 Your Personalized Study Plan — CIT-Sentinel` |
| Meeting Scheduled | Student | `📅 Meeting Scheduled — [Date] at [Time]` |

### Email Reliability

All email sends are wrapped in try/catch. If email delivery fails:
- Data still saves to MongoDB ✅
- Toast shows appropriate message ✅
- No crash ✅

---

## 🌍 SDG 4 Alignment

**Goal 4: Ensure inclusive and equitable quality education and promote lifelong learning opportunities for all.**

| SDG 4 Target | CIT-Sentinel Implementation |
|---|---|
| 4.1 — Free, equitable quality education | Early identification ensures no student is left behind |
| 4.5 — Eliminate gender disparities | Risk scoring is purely performance-based, not demographic |
| 4.a — Build quality education facilities | Digital infrastructure for academic intelligence |
| 4.b — Scholarships and support | At-risk students flagged for counseling and financial guidance |

### Projected Impact at CIT

| Metric | Before Sentinel | With Sentinel |
|---|---|---|
| Dropout Rate | ~8% | Target < 3% |
| Intervention Response Time | 4–6 weeks | < 1 week |
| At-risk detection accuracy | ~40% | ~94% |
| Parent notification speed | Monthly | Real-time |

---

## 🚀 Deployment

### Frontend — Vercel

```bash
# Connect GitHub repo to Vercel
# Set environment variables in Vercel dashboard:
VITE_API_URL=https://your-backend-url.railway.app
VITE_ANTHROPIC_API_KEY=your_key

# Auto-deploys on every push to main
```

Live URL: [https://cit-sentinal.vercel.app](https://cit-sentinal.vercel.app)

### Backend — Local / Railway / Render

**For local network sharing:**
```bash
# Set in backend/.env:
VITE_API_URL=http://YOUR_LOCAL_IP:3001

# Share access via:
http://YOUR_LOCAL_IP:8080
```

**For cloud deployment (Railway):**
```bash
# Add all .env variables to Railway dashboard
# Railway auto-detects Node.js and runs: npm start
# Add to package.json scripts:
"start": "node server.js"
```

### Network Configuration for Demo

```bash
# Find your local IP
ipconfig  # Windows
ifconfig  # Mac/Linux

# Allow firewall (Windows)
netsh advfirewall firewall add rule name="CIT-Sentinel" ^
  dir=in action=allow protocol=TCP localport=3001
```

---

## 🔧 Common Issues & Fixes

### Black Screen After Login

**Cause:** Backend offline, AuthContext crashes silently
**Fix:** Fallback credentials in AuthContext work without backend. Check browser console for errors.

### EADDRINUSE Port Error

```bash
# Windows — kill process on port 3001
for /f "tokens=5" %a in ('netstat -ano ^| findstr :3001') do taskkill /PID %a /F
```

### MongoDB Connection Failed

1. Check Atlas IP whitelist — must include `0.0.0.0/0`
2. Verify MONGODB_URI in `backend/.env`
3. Check Atlas cluster is not paused (free tier pauses after inactivity)

### Ollama Not Responding

Ollama runs as a Windows background service — `ollama serve` error "address already in use" means it's already running. That's correct — just use it directly.

```bash
# Verify Ollama is running
curl http://localhost:11434/api/tags
```

---

## 📊 Student Data Schema

```typescript
{
  id: string,                    // e.g. "CIT1ADS001"
  name: string,
  department: "AI & DS" | "CSE" | "ECE" | "Mechanical",
  year: 1 | 2 | 3 | 4,
  section: "A" | "B" | "C",
  attendance: number,            // 0-100
  theoryAttendance: number,      // 0-100
  labAttendance: number,         // 0-100
  iat1: number,                  // 0-50
  iat2: number,                  // 0-50
  model: number,                 // 0-100
  lmsActivity: number,           // 0-100
  hackathonWins: number,
  lateSubmissions: number,
  cgpa: number,                  // 0-10
  sentinelScore: number,         // AUTO-CALCULATED 0-100
  status: "Safe" | "At-Risk" | "Observation" | "Critical",  // AUTO-SET
  persona: string,               // Behavioural classification
  weeklyAttendance: [{week, percentage}],
  weeklyRiskTrend: [{week, score}],
  badges: string[],
  email: string,
  parentEmail: string,
  lastUpdated: Date
}
```

---

## 🏆 Hackathon Context

- **Event:** Internal Hackathon — Final Round Selected ✅
- **Track:** AI for Social Good / SDG Alignment
- **Team:** Chennai Institute of Technology — AI & DS Department
- **Timeline:** Built in one hackathon cycle
- **Status:** Fully functional with live MongoDB Atlas, real email system, and AI integration

---

## 📄 License

This project was built for academic and hackathon purposes at Chennai Institute of Technology.

---

## 🙏 Acknowledgements

- **Anthropic** — Claude Sonnet API for AI fallback
- **Meta** — Llama 3.2 for local AI inference via Ollama
- **MongoDB** — Atlas free tier for cloud database
- **Vercel** — Frontend deployment
- **shadcn/ui** — Component library
- **Recharts** — Data visualization

---

<div align="center">

**Built with ❤️ at Chennai Institute of Technology**

*"Most systems tell you a student has failed.*
*CIT-Sentinel tells you six weeks earlier — and tells you exactly what to do about it."*
</div>
