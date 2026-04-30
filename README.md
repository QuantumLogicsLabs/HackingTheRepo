# RepoMind UI — MERN Stack Frontend

A full-stack web interface for the **RepoMind** AI-powered PR bot. Users can sign up, submit repository instructions, and have the **SENDROOM bot** (a dedicated GitHub account configured in your server environment) open pull requests automatically.

---

## Architecture

```
repomind-ui/
├── client/          ← React + Vite frontend
│   └── src/
│       ├── pages/   ← LandingPage, LoginPage, SignupPage, Dashboard, NewJob, JobDetail, Settings
│       ├── components/ ← Layout (sidebar), StatusBadge
│       ├── context/ ← AuthContext (JWT-based auth)
│       └── utils/   ← Axios instance
│
└── server/          ← Express.js + MongoDB backend
    ├── models/      ← User, Job (Mongoose)
    ├── routes/      ← /api/auth, /api/jobs, /api/settings
    └── middleware/  ← JWT protect middleware
```

---

## Quick Start

### 1. Install dependencies

```bash
# From repo root
npm run install:all
```

### 2. Configure environment

```bash
cd server
cp .env.example .env
```

Edit `server/.env`:

```env
MONGO_URI=mongodb://localhost:27017/repomind
JWT_SECRET=your_super_secret_key

# 🤖 SENDROOM Bot — the GitHub account that opens PRs
REPOMIND_GITHUB_TOKEN=ghp_your_bot_token_here
REPOMIND_GITHUB_USERNAME=your-bot-username

# RepoMind FastAPI backend (run separately)
REPOMIND_API_URL=http://localhost:8000

# Optional: default OpenAI key for RepoMind
OPENAI_API_KEY=sk-...

PORT=5000
```

### 3. Start RepoMind FastAPI backend

```bash
# In the RepoMind Python project:
uvicorn api.main:app --reload --port 8000
```

### 4. Run the MERN app

```bash
# From repo root — starts both server (5000) and client (3000)
npm run dev
```

Open http://localhost:3000

---

## How it Works

1. User signs up / logs in on the web UI
2. User submits: **repo URL + instruction + optional branch/PR title**
3. Express server calls **RepoMind FastAPI** (`POST /run`) using the **SENDROOM bot token** (server-level env var — never exposed to users)
4. RepoMind agent clones the repo, plans changes with GPT-4o, applies them, and opens a PR
5. User polls for status via **Dashboard → Job Detail** (auto-refreshes every 5s while running)
6. User can send **refinement instructions** to iterate on the same PR

---

## API Routes

### Auth
- `POST /api/auth/signup` — register
- `POST /api/auth/login` — login, returns JWT
- `GET /api/auth/me` — current user

### Jobs
- `POST /api/jobs` — create new job (triggers RepoMind)
- `GET /api/jobs` — list all jobs for user
- `GET /api/jobs/:id` — job details
- `GET /api/jobs/:id/status` — poll status from RepoMind API
- `POST /api/jobs/:id/refine` — send follow-up instruction
- `DELETE /api/jobs/:id` — delete job

### Settings
- `GET /api/settings` — get user settings (tokens masked)
- `PUT /api/settings` — update github username / tokens

---

## Tech Stack

| Layer | Tech |
|-------|------|
| Frontend | React 18 + Vite + React Router v6 |
| Styling | Custom CSS with CSS variables (dark theme) |
| Backend | Express.js (ESM) |
| Database | MongoDB + Mongoose |
| Auth | JWT (7-day expiry) |
| HTTP | Axios |
| Bot Integration | Calls RepoMind FastAPI at `REPOMIND_API_URL` |

---

## SENDROOM Bot Setup

1. Create a dedicated GitHub account (e.g. `my-repomind-bot`)
2. Generate a PAT with `repo` scope
3. Set in `server/.env`:
   ```
   REPOMIND_GITHUB_TOKEN=ghp_bot_token
   REPOMIND_GITHUB_USERNAME=my-repomind-bot
   ```
4. The bot will be the author of all PRs — users never need to share their own tokens for PR creation

---

## License

MIT © HackingTheRepo Team
