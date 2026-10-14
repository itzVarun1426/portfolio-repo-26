# Varun Nagote Portfolio & Wall System - Progress Tracker

## Architectural Summary
- **Frontend**: React 18, Vite, Tailwind CSS, Framer Motion, HTML5 Canvas (Space Sky, Silky Mouse Trail, Interactive Tech Orbit, Drawing Canvas).
- **Backend**: Node.js, Express, PostgreSQL (`pg` raw parameterized SQL), Passport.js (Google & GitHub OAuth 2.0 with HTTP-only cookies), Helmet, Rate Limiter.
- **Database**: PostgreSQL with `users` and `wall_pins` (JSONB for vector drawing strokes).

## Database Schema Specification
```sql
CREATE TABLE IF NOT EXISTS users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) UNIQUE NOT NULL,
  avatar_url TEXT,
  provider VARCHAR(50) NOT NULL, -- 'google' | 'github'
  provider_user_id VARCHAR(255) NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
  UNIQUE(provider, provider_user_id)
);

CREATE TABLE IF NOT EXISTS wall_pins (
  id SERIAL PRIMARY KEY,
  user_id INT REFERENCES users(id) ON DELETE CASCADE,
  message VARCHAR(200) NOT NULL,
  drawing_data JSONB, -- Array of stroke objects: [{ color: "#ffffff", size: 2, points: [{x, y}, ...] }]
  pin_color VARCHAR(30) DEFAULT 'cyan',
  created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX IF NOT EXISTS idx_wall_pins_created_at ON wall_pins (created_at DESC);
```

## Task Checklist

### Phase 1: Environment & Project Scaffolding
- [x] Create project tracking documentation (`PROGRESS.md`)
- [x] Initialize `package.json` with scripts & dependencies
- [x] Setup Vite + React + Tailwind CSS configuration
- [x] Setup Server structure with Express & PostgreSQL pool setup

### Phase 2: Core Frontend UI Infrastructure
- [x] Data layer (`projects.js`, `experience.js`, `education.js`, `technologies.js`, `socialLinks.js`)
- [x] Cursor System: Reticle Target Snapper + Silky Inertia Mouse Trail
- [x] Space Sky Canvas Background (stars, particle glow, RAF pause on hidden tab)
- [x] Navigation Bar (Floating header, responsive mobile drawer, route indicator)

### Phase 3: Main Portfolio Sections (Re-engineered Concepts)
- [x] Hero Section (Display typography, satellite orbit indicator, technical status micro-labels)
- [x] About Section (Clean modern specs record, full-stack identity)
- [x] Projects Section (Interactive Planetary system cards with readouts & link triggers)
- [x] Experience Section (Constellation role cards & interactive timeline view with GDGC DYPCOE Lead)
- [x] Education Journey (Orbital timeline & constellation nodes: 10th, 12th, B.E. Computer Engineering)
- [x] Tech Stack Section (Interactive 2D Canvas/CSS orbital tech nodes with category filters)
- [x] Wall Preview Card (Teaser on homepage for `/wall`)
- [x] Contact & Socials (Futuristic space terminal layout with placeholders for links)
- [x] Minimal Footer

### Phase 4: Backend API & Wall Database System
- [x] Express server initialization, middleware (Helmet, CORS, Rate limiting, Session cookies)
- [x] PostgreSQL connection pool (`server/db/index.js`) & SQL migrations script
- [x] Passport.js OAuth setup (Google & GitHub strategies)
- [x] Wall Pins Controller (`GET /api/wall/pins`, `POST /api/wall/pins`, `DELETE /api/wall/pins/:id`, `GET /api/auth/me`)
- [x] Input validation (Server-side message constraints, max stroke limits for drawing JSONB)

### Phase 5: The Wall Frontend Experience (`/wall`)
- [x] Wall route setup in React Router (`/wall`)
- [x] Floating/Masonry space pin grid with pagination
- [x] Canvas Drawing Component (stroke recorder, clear, undo, color picker, JSON vector output)
- [x] OAuth Login & Pin Creation Modal
- [x] Vector Drawing Renderer (Renders JSONB strokes cleanly on cards)

### Phase 6: Performance, Accessibility & Testing
- [x] Preloader with real resource check (no artificial delay, hides < 300ms)
- [x] Touch device & `prefers-reduced-motion` detection
- [x] Error fallbacks for DB disconnected state / API failure
- [x] Production build verification & README setup guide

