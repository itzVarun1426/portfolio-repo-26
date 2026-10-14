# Varun Nagote — Developer Portfolio & Digital Wall System

A Cloud & DevOps Engineer portfolio and interactive space archive built for **Varun Nagote** (Full-Stack Developer).

Inspired by modern space/orbital aesthetics, re-engineered as a high-performance React SPA with a Node.js + PostgreSQL backend.

---

## Tech Stack

- **Frontend**: React 18, Vite, Tailwind CSS, Framer Motion, HTML5 Canvas (Starfield, Inertia Mouse Trail, Drawing Canvas)
- **Backend**: Node.js, Express
- **Database**: PostgreSQL (using `pg` raw parameterized SQL queries)
- **Authentication**: Google & GitHub OAuth 2.0 via Passport.js + HTTP-only sessions
- **Security**: Helmet, Rate Limiter, CORS protection, Input sanitization

---

## Quick Setup Instructions

### 1. Prerequisites
- Node.js (v18+)
- PostgreSQL installed & running

### 2. Environment Configuration
Copy `.env.example` to `.env`:
```bash
cp .env.example .env
```
Ensure your `DATABASE_URL` matches your local PostgreSQL setup:
```env
DATABASE_URL=postgres://postgres:password@localhost:5432/varun_portfolio
```

### 3. Install Dependencies
```bash
npm install
```

### 4. Initialize PostgreSQL Database Tables
Create your database in PostgreSQL (e.g. `varun_portfolio`), then run:
```bash
npm run db:init
```

### 5. Start Development Servers
Runs Vite frontend (`http://localhost:5173`) and Express backend (`http://localhost:5000`) concurrently:
```bash
npm start
```

---

## Key Features & Routes

- `/` — Single-page portfolio with Hero, About, Projects, Experience, Education Journey timeline, Tech Stack matrix, Digital Wall preview, and Contact section.
- `/wall` — Digital Wall page where visitors can view public pins, sign in via Google/GitHub OAuth, leave messages (max 200 chars), and create vector drawings on an HTML5 canvas.

---

## Production Build

```bash
npm run build
npm run server
```
