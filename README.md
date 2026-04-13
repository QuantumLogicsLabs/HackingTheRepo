> **Autonomous AI Developer Platform** - A fully scalable MERN stack application that intelligently analyzes repositories, learns from code patterns, and automatically submits high-quality Pull Requests.

[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](https://opensource.org/licenses/ISC)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D16.0.0-brightgreen)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-4.4%2B-green)](https://www.mongodb.com/)
[![React](https://img.shields.io/badge/React-18.3.1-blue)](https://reactjs.org/)

A cutting-edge AI platform that ingests your repositories, utilizes deep semantic memory, verifies generated code in secure sandboxes, and automatically submits precise Pull Requests with detailed explanations.

## ✨ Core Features

### 🧠 **Multi-Model LLM Fallback Chain**
Intelligent API cascading system that tries multiple models in sequence:
- `DeepSeek-Coder` → `Google Flash (OpenRouter)` → `Alibaba Qwen-Max` → `Puter.js Claude`
- Graceful fallback handling for rate limits and service outages
- Automatic model selection based on task complexity

### 🔒 **Secure Sandbox Execution**
- Isolated `.sandbox` environment for code testing
- Real-time `stdout`/`stderr` monitoring and analysis
- Iterative error correction with AI feedback loops
- Build script validation before any commits

### 🚀 **Autonomous CI/CD Pipeline**
- Intelligent branch creation with descriptive names
- Automated Pull Request generation with detailed commit messages
- Code review simulation before submission
- Integration with GitHub's API for seamless workflow

### 💾 **Deep Context Memory System**
- **Pinecone Vector Database** for semantic code search
- **Local Transformers** (`@xenova/transformers`) for on-device embedding
- **MongoDB Lesson Schema** for architectural pattern learning
- Prevents repetitive mistakes through intelligent memory

### ⏰ **Background Repository Monitoring**
- `node-cron` orchestrator with 5-minute intervals
- Multi-repository support with comma-separated configuration
- Automatic triggers for new commits and issues
- Configurable monitoring schedules

### 📊 **Real-Time Developer Dashboard**
- Modern React 18 interface with glassmorphism design
- WebSocket streaming (`Socket.io`) for live updates
- Interactive terminal with agent thought process visualization
- Job history and performance analytics

---

## 🚀 Quick Start

### 📋 Prerequisites

**Required:**
- **Node.js** >= 16.0.0
- **MongoDB** >= 4.4 (local or Atlas)
- **Git** for repository operations

**API Keys Needed:**
- [GitHub Personal Access Token](https://github.com/settings/tokens) (with `repo` scopes)
- At least one AI service API key (see configuration below)

### 🔧 1. Backend Configuration

Navigate to the `backend/` directory and set up your environment:

```bash
cd backend
cp .env.example .env
```

**Configure your `.env` file:**

```env
# GitHub Configuration
GITHUB_TOKEN=your_github_personal_access_token_here
GITHUB_REPOS=username/repo1,username/repo2

# AI Service Keys (System will try them in this order)
DEEPSEEK_API_KEY=your_deepseek_api_key_here
OPENROUTER_API_KEY=your_openrouter_api_key_here
QWEN_API_KEY=your_qwen_api_key_here
PUTER_API_KEY=your_puter_api_key_here

# Database Configuration
MONGO_URI=mongodb+srv://user:pass@cluster.mongodb.net/quantum-code-agent
# OR for local development:
# MONGO_URI=mongodb://127.0.0.1:27017/quantum-code-agent

# Optional: Vector Memory
PINECONE_API_KEY=your_pinecone_api_key_here
PINECONE_INDEX_NAME=your_pinecone_index_name_here
```

### 📦 2. Install Dependencies

Install dependencies for both backend and frontend:

```bash
# Backend dependencies
cd backend
npm install

# Frontend dependencies
cd ../frontend
npm install

# Or install from root (if package.json has scripts)
cd ..
npm install
npm run server
npm run client
```

### 🏃 3. Run the Platform

**Option A: Concurrent Development (Recommended)**
```bash
# From root directory
npm run dev
```

**Option B: Separate Terminals**

Terminal 1 - Backend Server:
```bash
cd backend
npm run dev
# Server runs on http://localhost:5000
```

Terminal 2 - Frontend Dashboard:
```bash
cd frontend
npm start
# Dashboard runs on http://localhost:3000
```

**Access Points:**
- 🎯 **Frontend Dashboard**: http://localhost:3000
- 🔧 **Backend API**: http://localhost:5000
- 📊 **Health Check**: http://localhost:5000/api/health

## 🏗️ Architecture Overview

```bash
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Frontend      │    │    Backend       │    │  External APIs  │
│  (React 18)     │◄──►│   (Node.js)      │◄──►│  (GitHub, AI)   │
│                 │    │                  │    │                 │
│ • Dashboard     │    │ • Socket.io      │    │ • DeepSeek      │
│ • Real-time UI  │    │ • Express        │    │ • OpenRouter    │
│ • Job History   │    │ • MongoDB        │    │ • Qwen          │
└─────────────────┘    │ • Pinecone       │    │ • Puter         │
                       └──────────────────┘    └─────────────────┘
```

### 📁 Core Services

| Service | File | Description |
|---------|------|-------------|
| **🤖 Agent Controller** | `agentController.js` | Main orchestrator for GitHub fetching, vector memory, sandbox loops, and PR automation |
| **🧠 Vector Service** | `vectorService.js` | Code chunking and semantic similarity search using Pinecone |
| **🔒 Sandbox Service** | `sandboxService.js` | Secure OS-level wrapper for iterative code testing |
| **⏰ Cron Service** | `cronService.js` | Automated repository monitoring and scheduling |
| **🤖 AI Service** | `aiService.js` | Multi-model LLM integration and prompt engineering |
| **📊 Job Manager** | `jobController.js` | Job lifecycle management and persistence |

### 🗄️ Database Schema

- **Jobs**: Track repository analysis progress and results
- **Lessons**: Store learned architectural patterns and decisions
- **Vectors**: Semantic embeddings for code similarity search

---

## 🔧 Development Scripts

```json
{
  "scripts": {
    "start": "node backend/server.js",
    "dev": "concurrently \"npm run server\" \"npm run client\"",
    "server": "cd backend && npm run dev",
    "client": "cd frontend && npm run dev",
    "build": "cd frontend && npm run build",
    "test": "cd backend && npm test && cd ../frontend && npm test"
  }
}
```

---

## 🐛 Troubleshooting

### Common Issues

**MongoDB Connection Error**
```bash
# For local MongoDB, ensure it's running:
mongod

# Check connection string format
MONGO_URI=mongodb://127.0.0.1:27017/quantum-code-agent
```

**Port Already in Use**
```bash
# Kill processes on ports 3000 and 5000
npx kill-port 3000 5000
```

**API Key Issues**
- Verify all API keys are correctly set in `.env`
- Check GitHub token has `repo` permissions
- Ensure at least one AI service API key is valid

### Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `GITHUB_TOKEN` | ✅ | GitHub Personal Access Token |
| `GITHUB_REPOS` | ✅ | Comma-separated repository list |
| `MONGO_URI` | ✅ | MongoDB connection string |
| `DEEPSEEK_API_KEY` | ⚠️ | DeepSeek AI API key |
| `OPENROUTER_API_KEY` | ⚠️ | OpenRouter API key |
| `QWEN_API_KEY` | ⚠️ | Alibaba Qwen API key |
| `PUTER_API_KEY` | ⚠️ | Puter.js API key |
| `PINECONE_API_KEY` | ❌ | Pinecone vector DB key (optional) |

*⚠️ At least one AI service key is required*

---

## 📄 License

This project is licensed under the **ISC License** - see the [LICENSE](LICENSE) file for details.

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📞 Support

- 📧 **Email**: support@quantumlogicslabs.com
- 🐛 **Issues**: [GitHub Issues](https://github.com/QuantumLogicsLabs/HackingTheRepo/issues)
- 💬 **Discussions**: [GitHub Discussions](https://github.com/QuantumLogicsLabs/HackingTheRepo/discussions)

---

*Built with ❤️ by the Quantum AI Code Agent system*