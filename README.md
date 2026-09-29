# CareerHub — Modern Recruitment Platform (Task 3)

> A modern recruitment platform connecting job seekers and companies through job listings, applications, candidate profiles, and recruitment dashboards.

---

## 🚀 Project Overview

**CareerHub** simplifies the hiring process by bringing candidates and recruiters together on one centralized, high-performance platform:
- **Candidates** can search and filter verified jobs, upload resumes (PDF/DOCX), apply for positions with one click, and track their application pipeline status in real time.
- **Recruiters & Employers** can publish and manage job postings, review applicant profiles, download attached resumes, score candidates, and guide them through an interactive **ATS Kanban Pipeline** (`Applied` → `Screening` → `Interview` → `Offer Extended` → `Hired`).

---

## 🛠️ Technology Stack

- **Frontend & Framework**: [Next.js 14](https://nextjs.org/) (App Router, React 18, TypeScript)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/) with modern responsive UI and sleek gradients
- **Icons**: [Lucide React](https://lucide.dev/)
- **Database & ORM**: [PostgreSQL](https://www.postgresql.org/) configured with [Prisma ORM](https://www.prisma.io/) (`prisma/schema.prisma`)
- **Dual-Mode Data Layer**: Production-ready PostgreSQL schema + automatic local development fallback store for zero-setup instant local testing
- **File Storage**: Multi-provider storage engine (`/api/upload`) supporting local disk uploads (`public/uploads`) and modular cloud storage (AWS S3 / Supabase / Cloudinary)

---

## 🌟 Key Features

### 1. Job Seeker & Candidate Experience
- **Interactive Job Search & Filtering**: Filter by keywords, employment type (Full-Time, Remote, Contract, Part-Time), category, experience level, and minimum annual salary slider.
- **Job Details View**: Comprehensive company overview, responsibilities, technical requirements, perks, and salary breakdown.
- **1-Click Application Flow**: Quick Apply modal with pre-filled candidate profile, cover note editor, and resume file upload.
- **Candidate Dashboard**:
  - **Live Application Pipeline Tracker**: Visual progress bar tracking each application across `APPLIED`, `SCREENING`, `INTERVIEW`, `OFFER`, and `HIRED` stages.
  - **Recruiter Updates**: View real-time feedback and recruiter notes directly on applications.
  - **Profile & Resume Builder**: Edit professional headline, bio, experience years, and interactive skill tags.

### 2. Employer & Recruiter ATS Experience
- **Recruitment KPI Metrics**: Real-time counter cards for Active Openings, Total Candidates, Interviews In Progress, and Hired Candidates.
- **Interactive ATS Kanban Board**: Visual drag/move pipeline columns to promote candidates across stages with single-click actions.
- **Candidate Inspector & Resume Reviewer**: Inspect applicant details, read cover statements, preview/download attached resumes, assign star ratings (1–5), and record internal recruiter notes.
- **Job Posting Management**: Create new job openings with salary ranges, toggle jobs between active and paused, and monitor applicant counts.

### 3. Authentication & Account Access
- **Dedicated Login (`/login`)**:
  - Secure credential login (Email & Password).
  - 1-Click Instant Demo Login buttons: **Candidate (Alex Morgan)** and **Recruiter (Sarah Chen)**.
  - "Remember me" persistence and intuitive error messages.
- **Dedicated Registration (`/register`)**:
  - Dual-mode registration for **Job Seekers (Candidates)** and **Employers (Recruiters)**.
  - Recruiter accounts capture company & organization details.
  - Automatic session initialization and instant redirect to the appropriate dashboard.
- **Auth State in Navbar**:
  - Real-time user avatar, name, and role badge.
  - Sign Out button and guest Sign In / Sign Up triggers.

---

## 📁 Project Directory Structure

```text
job portal/
├── prisma/
│   ├── schema.prisma              # PostgreSQL schema (User, Profile, Job, Application)
│   └── seed.js                    # Database seed script for PostgreSQL
├── public/
│   └── uploads/                   # Storage destination for uploaded candidate resumes
├── src/
│   ├── app/
│   │   ├── api/
│   │   │   ├── applications/      # Applications API (GET list, POST new application)
│   │   │   │   ├── route.ts
│   │   │   │   └── [id]/route.ts  # Application stage & notes update (PATCH)
│   │   │   ├── jobs/              # Jobs API (GET search & filter, POST create job)
│   │   │   │   ├── route.ts
│   │   │   │   └── [id]/route.ts  # Single job retrieval, update, delete
│   │   │   ├── profile/           # Candidate profile API (GET, PUT)
│   │   │   │   └── route.ts
│   │   │   ├── stats/             # Recruiter dashboard KPI stats API
│   │   │   │   └── route.ts
│   │   │   └── upload/            # Resume & document file upload handler
│   │   │       └── route.ts
│   │   ├── dashboard/
│   │   │   ├── candidate/page.tsx # Candidate application tracker & profile builder
│   │   │   └── recruiter/page.tsx # Recruiter ATS Kanban board & jobs manager
│   │   ├── jobs/
│   │   │   ├── page.tsx           # Public jobs directory with sidebar filters
│   │   │   └── [id]/page.tsx      # Job details page with apply modal
│   │   ├── post-job/page.tsx      # Recruiter job posting form
│   │   ├── globals.css            # Tailwind directives & global styling
│   │   ├── layout.tsx             # Root layout with Navbar and Footer
│   │   └── page.tsx               # Homepage hero, search bar & featured jobs
│   ├── components/
│   │   ├── jobs/
│   │   │   ├── ApplyModal.tsx     # Quick apply modal with resume upload
│   │   │   ├── JobCard.tsx        # Responsive job card component
│   │   │   └── JobFilters.tsx     # Filter sidebar (category, salary, type)
│   │   ├── layout/
│   │   │   ├── Footer.tsx         # Platform footer with tech stack details
│   │   │   └── Navbar.tsx         # Sticky navigation with role switcher
│   │   ├── recruiter/
│   │   │   ├── ATSKanban.tsx      # Recruiter ATS Kanban board
│   │   │   └── CandidateModal.tsx # Candidate resume & pipeline inspector
│   │   └── ui/
│   │       ├── Badge.tsx          # Reusable status badges
│   │       └── StatsCard.tsx      # Metric cards
│   └── lib/
│       ├── db.ts                  # Database & repository service
│       ├── mockData.ts            # Realistic initial jobs and applicants data
│       ├── storage.ts             # File upload and storage service
│       ├── types.ts               # TypeScript data models and interfaces
│       └── utils.ts               # Formatting helpers (salary, badges, cn)
├── .env                           # Local environment configuration
├── .env.example                   # Environment variable template
├── .gitignore                     # Git ignore rules
├── next.config.js                 # Next.js configuration
├── package.json                   # Project dependencies and run scripts
├── postcss.config.js              # PostCSS configuration
├── tailwind.config.ts             # Tailwind CSS configuration
└── tsconfig.json                  # TypeScript configuration
```

---

## ⚡ Quick Start Guide

### 1. Prerequisites
Ensure you have [Node.js](https://nodejs.org/) (v18.x or newer) installed.

### 2. Install Dependencies
```bash
npm install
```

### 3. Start Development Server
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) in your web browser.

---

## 🗄️ PostgreSQL Setup (Optional / Production)

The app comes configured with a complete Prisma schema for PostgreSQL. To connect a live PostgreSQL database (e.g. Supabase, Neon, AWS RDS, or local Docker):

1. Open `.env` and set your `DATABASE_URL`:
   ```env
   DATABASE_URL="postgresql://postgres:password@localhost:5432/careerhub?schema=public"
   ```

2. Push the schema to your PostgreSQL database:
   ```bash
   npx prisma db push
   ```

3. Optionally seed the database:
   ```bash
   npm run prisma:seed
   ```

4. View and manage database records with Prisma Studio:
   ```bash
   npx prisma studio
   ```

---

## 🌐 API Endpoints Reference

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/jobs` | Retrieve all jobs (supports `query`, `category`, `type`, `location`, `minSalary`) |
| `POST` | `/api/jobs` | Create and publish a new job opening |
| `GET` | `/api/jobs/[id]` | Retrieve single job details by ID |
| `PUT` | `/api/jobs/[id]` | Update job details or toggle active status |
| `DELETE` | `/api/jobs/[id]` | Remove a job listing |
| `GET` | `/api/applications` | List applications (filterable by `candidateId` or `jobId`) |
| `POST` | `/api/applications` | Submit a candidate application with resume |
| `PATCH` | `/api/applications/[id]` | Update applicant stage, recruiter notes, or rating |
| `POST` | `/api/upload` | Upload resume file (PDF, DOC, DOCX) |
| `GET` | `/api/profile` | Retrieve candidate profile |
| `PUT` | `/api/profile` | Update candidate profile and skills |
| `GET` | `/api/stats` | Retrieve recruiter dashboard KPI metrics |
