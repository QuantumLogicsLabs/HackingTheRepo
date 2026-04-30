<div align="center">

<!-- HERO BANNER -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:6366f1,100:a855f7&height=200&section=header&text=HackingTheRepo&fontSize=60&fontColor=ffffff&fontAlignY=38&desc=AI-Powered%20Code%20Agent%20%E2%80%94%20Describe%20it.%20Ship%20it.&descAlignY=58&descSize=18" width="100%"/>

<br/>

<p>
  <a href="https://github.com/QuantumLogicsLabs/HackingTheRepo/stargazers">
    <img src="https://img.shields.io/github/stars/QuantumLogicsLabs/HackingTheRepo?style=for-the-badge&color=f59e0b&labelColor=1e1e2e" alt="Stars"/>
  </a>
  <a href="https://github.com/QuantumLogicsLabs/HackingTheRepo/network/members">
    <img src="https://img.shields.io/github/forks/QuantumLogicsLabs/HackingTheRepo?style=for-the-badge&color=6366f1&labelColor=1e1e2e" alt="Forks"/>
  </a>
  <a href="https://github.com/QuantumLogicsLabs/HackingTheRepo/issues">
    <img src="https://img.shields.io/github/issues/QuantumLogicsLabs/HackingTheRepo?style=for-the-badge&color=ef4444&labelColor=1e1e2e" alt="Issues"/>
  </a>
  <a href="https://github.com/QuantumLogicsLabs/HackingTheRepo/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/QuantumLogicsLabs/HackingTheRepo?style=for-the-badge&color=22c55e&labelColor=1e1e2e" alt="License"/>
  </a>
</p>

<p>
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB"/>
  <img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white"/>
  <img src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white"/>
  <img src="https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white"/>
  <img src="https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white"/>
  <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white"/>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white"/>
  <img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white"/>
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white"/>
</p>

<br/>

> **HackingTheRepo** is an AI-powered developer tool that lets you describe a code change in plain English — and automatically clones your GitHub repo, plans the edits, rewrites the code, and opens a Pull Request. No scaffolding. No boilerplate. Just ship.

<br/>

</div>

---

## 📖 Table of Contents

- [✨ What It Does](#-what-it-does)
- [🏗️ Architecture](#️-architecture)
- [📁 Project Structure](#-project-structure)
- [⚙️ Prerequisites](#️-prerequisites)
- [🚀 Running Locally — Full Guide](#-running-locally--full-guide)
  - [1 · Clone the Monorepo](#1--clone-the-monorepo)
  - [2 · Set Up RepoMind (AI Agent)](#2--set-up-repomind-ai-agent)
  - [3 · Set Up the Backend (Node.js API)](#3--set-up-the-backend-nodejs-api)
  - [4 · Set Up the Frontend (React)](#4--set-up-the-frontend-react)
  - [5 · Run Everything](#5--run-everything)
- [🐳 Docker (RepoMind Only)](#-docker-repomind-only)
- [🔐 Environment Variables Reference](#-environment-variables-reference)
- [🗺️ API Reference](#️-api-reference)
- [🧪 Running Tests](#-running-tests)
- [🤝 Contributing](#-contributing)

---

## ✨ What It Does

HackingTheRepo gives every developer a **personal AI coding agent** that works directly on GitHub repositories.

```
You type:   "Add input validation to all API routes and write tests for them"
It does:    ✅ Clones your repo
            ✅ Plans the changes step by step
            ✅ Rewrites the relevant files
            ✅ Pushes to a new branch
            ✅ Opens a PR with a full diff summary
```

| Feature              | Description                                                          |
| -------------------- | -------------------------------------------------------------------- |
| 🤖 **AI Agent**      | LangChain-powered planner + executor that understands your codebase  |
| 🔀 **Auto PR**       | Creates a real GitHub Pull Request with a human-readable description |
| 🔁 **Refinements**   | Send follow-up instructions to iterate on the same job               |
| 📊 **Job Dashboard** | Track every job — queued, running, completed, failed                 |
| 🔒 **Auth**          | JWT-based user accounts; each user brings their own API keys         |
| 🐳 **Docker-ready**  | RepoMind ships with a `Dockerfile` for zero-config deployment        |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        Browser / User                           │
└──────────────────────────┬──────────────────────────────────────┘
                           │  HTTP
┌──────────────────────────▼──────────────────────────────────────┐
│              Frontend  (React + Vite)  :5173                    │
│   LandingPage · AuthPage · Dashboard · JobDetail · Settings     │
└──────────────────────────┬──────────────────────────────────────┘
                           │  REST API
┌──────────────────────────▼──────────────────────────────────────┐
│              Backend  (Node.js + Express)  :5000                │
│   /api/auth  ·  /api/jobs  ·  /api/settings                    │
│   MongoDB (Mongoose)  ·  JWT Auth Middleware                    │
└──────────────────────────┬──────────────────────────────────────┘
                           │  HTTP (job dispatch)
┌──────────────────────────▼──────────────────────────────────────┐
│              RepoMind  (Python + FastAPI)  :8000                │
│   agent/planner  ·  agent/executor  ·  agent/chain             │
│   tools: code_parser · diff_generator · github_tool · pr_tool  │
└──────────────────────────┬──────────────────────────────────────┘
                           │
              ┌────────────┴────────────┐
              │                         │
    ┌─────────▼──────────┐   ┌─────────▼──────────┐
    │   OpenAI GPT-4o    │   │   GitHub REST API   │
    │  (code generation) │   │  (clone · push · PR)│
    └────────────────────┘   └────────────────────┘
```

**Three independent services, all talking REST:**

| Service      | Stack                      | Port   | Repo                                                                                    |
| ------------ | -------------------------- | ------ | --------------------------------------------------------------------------------------- |
| **Frontend** | React, Vite                | `5173` | [HackingTheRepo-Frontend](https://github.com/QuantumLogicsLabs/HackingTheRepo-Frontend) |
| **Backend**  | Node.js, Express, MongoDB  | `5000` | [HackingTheRepo-Backend](https://github.com/QuantumLogicsLabs/HackingTheRepo-Backend)   |
| **RepoMind** | Python, FastAPI, LangChain | `8000` | [RepoMind](https://github.com/QuantumLogicsLabs/RepoMind)                               |

---

## 📁 Project Structure

```
HackingTheRepo/                 ← Monorepo root
├── frontend/                   ← React app (git submodule)
│   └── src/
│       ├── components/         ← Layout, StatusBadge
│       ├── context/            ← AuthContext (JWT state)
│       ├── pages/              ← Landing, Auth, Dashboard, JobDetail, Settings, NewJob
│       └── utils/api.js        ← Axios wrapper for backend calls
│
├── backend/                    ← Express API (git submodule)
│   ├── middleware/auth.js      ← JWT protect middleware
│   ├── models/
│   │   ├── User.js             ← User schema (bcrypt hashed passwords)
│   │   └── Job.js              ← Job schema (status, prUrl, refinements…)
│   └── routes/
│       ├── auth.js             ← /signup · /login · /me
│       ├── jobs.js             ← CRUD + refine + poll
│       └── settings.js         ← GitHub token / OpenAI key management
│
└── repomind/                   ← AI agent (git submodule)
    ├── agent/
    │   ├── planner.py          ← Breaks instruction → ordered plan steps
    │   ├── executor.py         ← Runs each step against the cloned repo
    │   ├── chain.py            ← LangChain pipeline wiring
    │   └── memory.py           ← Conversation memory for refinements
    ├── tools/
    │   ├── github_tool.py      ← Clone / push operations via GitPython
    │   ├── pr_tool.py          ← Opens PR via PyGithub
    │   ├── code_parser.py      ← Tree-sitter AST analysis
    │   ├── diff_generator.py   ← Human-readable diff summaries
    │   └── test_executor.py    ← Runs existing test suites in sandbox
    ├── api/
    │   ├── main.py             ← FastAPI app entry point
    │   ├── routes.py           ← POST /jobs · GET /jobs/{id}
    │   └── schemas.py          ← Pydantic request/response models
    └── utils/job_manager.py    ← In-memory job store (UUID-keyed)
```

---

## ⚙️ Prerequisites

Make sure the following are installed before you begin:

| Tool                    | Version                    | Check              |
| ----------------------- | -------------------------- | ------------------ |
| **Node.js**             | ≥ 18.x                     | `node -v`          |
| **npm**                 | ≥ 9.x                      | `npm -v`           |
| **Python**              | ≥ 3.11                     | `python --version` |
| **pip**                 | latest                     | `pip --version`    |
| **Git**                 | any recent                 | `git --version`    |
| **MongoDB**             | ≥ 6.x (local) or Atlas URI | —                  |
| **Docker** _(optional)_ | ≥ 24.x                     | `docker -v`        |

You will also need:

- An **OpenAI API key** (GPT-4o recommended)
- A **GitHub Personal Access Token** with `repo` + `workflow` scopes

---

## 🚀 Running Locally — Full Guide

### 1 · Clone the Monorepo

The project uses **git submodules** for the three services. A regular `git clone` will leave the submodule folders empty — use the flag below to pull everything in one shot.

```bash
git clone --recurse-submodules https://github.com/QuantumLogicsLabs/HackingTheRepo.git
cd HackingTheRepo
```

> **Already cloned without the flag?** Run this to catch up:
>
> ```bash
> git submodule update --init --recursive
> ```

---

### 2 · Set Up RepoMind (AI Agent)

RepoMind is the Python FastAPI service that powers the AI agent. It must be running before the backend can dispatch jobs.

```bash
cd repomind
```

#### 2a · Create & activate a virtual environment

```bash
# macOS / Linux
python3 -m venv .venv
source .venv/bin/activate

# Windows (PowerShell)
python -m venv .venv
.venv\Scripts\Activate.ps1
```

#### 2b · Install dependencies

```bash
pip install -e ".[dev]"
```

This installs FastAPI, Uvicorn, LangChain, GitPython, PyGithub, Tree-sitter, and all dev tools (`pytest`, `black`, `ruff`, `mypy`).

#### 2c · Configure environment variables

```bash
cp .env.example .env
```

Open `.env` and fill in your values:

```env
# ── LLM ──────────────────────────────────────────────────────────
OPENAI_API_KEY=sk-...          # Your OpenAI key
LLM_MODEL=gpt-4o               # or gpt-4-turbo, gpt-3.5-turbo
MAX_PLAN_STEPS=15              # Max agent steps per job

# ── GitHub ───────────────────────────────────────────────────────
GITHUB_TOKEN=ghp_...           # PAT with repo + workflow scopes
GITHUB_USERNAME=your-username  # Your GitHub username

# ── App ──────────────────────────────────────────────────────────
APP_ENV=development
LOG_LEVEL=INFO
```

#### 2d · Start the FastAPI server

```bash
uvicorn api.main:app --host 0.0.0.0 --port 8000 --reload
```

> ✅ RepoMind is live at **http://localhost:8000**
> Interactive docs available at **http://localhost:8000/docs**

---

### 3 · Set Up the Backend (Node.js API)

Open a **new terminal tab** and navigate to the backend:

```bash
cd HackingTheRepo/backend
```

#### 3a · Install dependencies

```bash
npm install
```

#### 3b · Configure environment variables

```bash
cp .env.example .env
```

Open `.env` and set:

```env
# ── Server ───────────────────────────────────────────────────────
PORT=5000
NODE_ENV=development

# ── Database ─────────────────────────────────────────────────────
MONGO_URI=mongodb://localhost:27017/hackingrepo
# OR use MongoDB Atlas:
# MONGO_URI=mongodb+srv://<user>:<pass>@cluster.mongodb.net/hackingrepo

# ── Auth ─────────────────────────────────────────────────────────
JWT_SECRET=your_super_secret_jwt_key_change_this

# ── RepoMind Agent ───────────────────────────────────────────────
REPOMIND_URL=http://localhost:8000
```

#### 3c · Start MongoDB (if running locally)

```bash
# macOS (Homebrew)
brew services start mongodb-community

# Linux (systemd)
sudo systemctl start mongod

# Windows
net start MongoDB
```

#### 3d · Start the backend server

```bash
npm run dev
# or: node index.js
```

> ✅ Backend API is live at **http://localhost:5000**

---

### 4 · Set Up the Frontend (React)

Open a **third terminal tab**:

```bash
cd HackingTheRepo/frontend
```

#### 4a · Install dependencies

```bash
npm install
```

#### 4b · Configure the API base URL

The frontend uses `src/utils/api.js` as its API wrapper. By default it points to `http://localhost:5000`. If you changed the backend port, update it there.

No `.env` is strictly required for local development, but you can create one:

```env
VITE_API_URL=http://localhost:5000
```

#### 4c · Start the dev server

```bash
npm run dev
```

> ✅ Frontend is live at **http://localhost:5173**

---

### 5 · Run Everything

Once all three services are running, open your browser and go to:

```
http://localhost:5173
```

**First-time setup flow:**

```
1.  Sign Up → create your account
2.  Go to Settings → add your GitHub Token and OpenAI API Key
3.  Dashboard → click "New Job"
4.  Enter:  · GitHub repo URL
            · Natural language instruction
            · Branch name
            · PR title
5.  Hit Submit → watch the job run in real time
6.  When done → click the PR link to review AI-generated code on GitHub 🎉
```

**Quick sanity checks:**

```bash
# Is RepoMind healthy?
curl http://localhost:8000/docs

# Is the backend healthy?
curl http://localhost:5000/api/auth/me   # expects 401 — that's correct

# Frontend compiles without errors?
# Check the Vite terminal output
```

---

## 🐳 Docker (RepoMind Only)

RepoMind ships with a production-ready `Dockerfile`. Run it in isolation if you prefer not to install Python locally.

```bash
cd repomind

# Build the image
docker build -t repomind:latest .

# Run the container (pass env vars via --env-file)
docker run -d \
  --name repomind \
  --env-file .env \
  -p 8000:8000 \
  repomind:latest
```

> ⚠️ The Node.js backend and React frontend don't have Dockerfiles yet. Contributions welcome!

---

## 🔐 Environment Variables Reference

### RepoMind (`repomind/.env`)

| Variable          | Required | Default       | Description                          |
| ----------------- | -------- | ------------- | ------------------------------------ |
| `OPENAI_API_KEY`  | ✅       | —             | OpenAI API key for GPT-4o            |
| `LLM_MODEL`       | ❌       | `gpt-4o`      | LLM model name                       |
| `MAX_PLAN_STEPS`  | ❌       | `15`          | Max steps the agent can take per job |
| `GITHUB_TOKEN`    | ✅       | —             | GitHub PAT (repo + workflow scopes)  |
| `GITHUB_USERNAME` | ✅       | —             | Your GitHub username                 |
| `APP_ENV`         | ❌       | `development` | `development` or `production`        |
| `LOG_LEVEL`       | ❌       | `INFO`        | Python log level                     |

### Backend (`backend/.env`)

| Variable       | Required | Default                 | Description                 |
| -------------- | -------- | ----------------------- | --------------------------- |
| `PORT`         | ❌       | `5000`                  | Express server port         |
| `MONGO_URI`    | ✅       | —                       | MongoDB connection string   |
| `JWT_SECRET`   | ✅       | —                       | Secret key for signing JWTs |
| `REPOMIND_URL` | ✅       | `http://localhost:8000` | RepoMind FastAPI base URL   |
| `NODE_ENV`     | ❌       | `development`           | Node environment            |

---

## 🗺️ API Reference

### Backend (Express) — Base: `http://localhost:5000`

#### Auth Routes

| Method | Endpoint           | Auth | Description              |
| ------ | ------------------ | ---- | ------------------------ |
| `POST` | `/api/auth/signup` | ❌   | Register a new user      |
| `POST` | `/api/auth/login`  | ❌   | Login and receive JWT    |
| `GET`  | `/api/auth/me`     | ✅   | Get current user profile |

#### Job Routes

| Method | Endpoint               | Auth | Description                    |
| ------ | ---------------------- | ---- | ------------------------------ |
| `POST` | `/api/jobs`            | ✅   | Create and dispatch a new job  |
| `GET`  | `/api/jobs`            | ✅   | List all jobs for current user |
| `GET`  | `/api/jobs/:id`        | ✅   | Get job details + status       |
| `POST` | `/api/jobs/:id/refine` | ✅   | Send a refinement instruction  |

#### Settings Routes

| Method | Endpoint        | Auth | Description                      |
| ------ | --------------- | ---- | -------------------------------- |
| `PUT`  | `/api/settings` | ✅   | Update GitHub token / OpenAI key |

### RepoMind (FastAPI) — Base: `http://localhost:8000`

| Method | Endpoint         | Description              |
| ------ | ---------------- | ------------------------ |
| `POST` | `/jobs`          | Submit a new agent job   |
| `GET`  | `/jobs/{job_id}` | Poll job status + result |

> 📖 Full interactive Swagger docs at **http://localhost:8000/docs**

---

## 🧪 Running Tests

### RepoMind (Python)

```bash
cd repomind
source .venv/bin/activate   # activate venv if not already

# Run all tests
pytest

# With coverage report
pytest --cov=. --cov-report=term-missing

# Run a specific test file
pytest tests/test_agent.py -v
```

### Linting & Formatting

```bash
# Format with black
black .

# Lint with ruff
ruff check .

# Type-check with mypy
mypy .
```

---

## 🤝 Contributing

Contributions are what make open source amazing. Any contribution you make is **greatly appreciated**.

```bash
# 1. Fork the repo on GitHub
# 2. Clone your fork
git clone --recurse-submodules https://github.com/YOUR_USERNAME/HackingTheRepo.git

# 3. Create a feature branch
git checkout -b feat/your-feature-name

# 4. Make your changes and commit
git commit -m "feat: add your amazing feature"

# 5. Push to your fork
git push origin feat/your-feature-name

# 6. Open a Pull Request on GitHub
```

**Please make sure to:**

- Follow the existing code style (`black` for Python, consistent JS formatting for Node/React)
- Add or update tests for any new functionality
- Update this README if you add new env vars or change ports

---

<div align="center">

<br/>

**Built with ❤️ by [QuantumLogicsLabs](https://github.com/QuantumLogicsLabs)**

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:a855f7,100:6366f1&height=100&section=footer" width="100%"/>

</div>
