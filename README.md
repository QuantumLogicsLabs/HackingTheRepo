# Quantum Code Agent

A fully autonomous, scalable AI developer platform built on the MERN stack. Designed to ingest your repositories, utilize deep semantic memory, verify its own generated code in a secure sandbox, and automatically submit precise Pull Requests.

## Core Features

- **Multi-Model LLM Fallback**: Hardcoded to try a cascading array of open and proprietary intelligence APIs (`DeepSeek-Coder` -> `Google Flash via OpenRouter` -> `Alibaba Qwen-Max` -> `Puter.js Claude`). The agent gracefully falls back if any specific API is rate-limited or unresponsive.
- **Agentic Sandbox Execution (Phase 2)**: The AI does not blindly commit. It initializes a local `.sandbox` environment, runs your build scripts or `npm test`, reads the `stdout`/`stderr` terminal outputs, and feeds it iteratively back into its own prompt to fix errors automatically.
- **Autonomous CI/CD (Phase 4)**: Once the AI approves the code internally, it uses `@octokit/rest` to push files to a temporary branch and automatically opens a sophisticated Pull Request against your default branch detailing its algorithmic decisions.
- **Deep Context Memory (Phase 1)**: Integrated with **Pinecone Vector Database** and local `@xenova/transformers` for free code embedding. It also utilizes a MongoDB `Lesson` schema to permanently remember project-specific architectural guidelines, preventing the AI from repeating the same hallucinatory mistakes.
- **Background Multi-Repo Sync**: Connect a comma-separated list of your repositories in the environment variables. A `node-cron` orchestrator checks every 5 minutes for new commits and automatically triggers deep research and bug-hunting sweeps.
- **Real-Time Developer Dashboard**: Built explicitly with Create React App and raw, premium CSS glassmorphism. It uses WebSockets (`Socket.io`) to stream exact sandbox execution logs and agent thought processes in real-time.

---

## Quickstart & Installation

**Prerequisites:**
- Node.js installed
- MongoDB installed and running locally on port 27017
- [GitHub Personal Access Token](https://github.com/settings/tokens) (with `repo` scopes)

### 1. Backend Configuration
Navigate to the `backend/` directory and copy the `.env.example` into a `.env` file:
\`\`\`bash
cd backend
cp .env.example .env
\`\`\`
Populate your `.env` with the necessary API keys, database connection, and arbitrary GitHub repositories you wish the AI to monitor.

### 2. Install Dependencies
Install dependencies concurrently for the workspace:
\`\`\`bash
cd backend
npm install
cd ../frontend
npm install
\`\`\`

### 3. Run the Platform
You can start the backend and frontend simultaneously with a concurrent script if available, or just start both processes:

Terminal 1 (Backend Node Server):
\`\`\`bash
cd backend
npm run dev
\`\`\`

Terminal 2 (React Developer Dashboard):
\`\`\`bash
cd frontend
npm start
\`\`\`

## Architecture Modules

*   **`agentController.js`**: The main orchestrator connecting GitHub fetching, Vector memory retrieval, Sandbox loops, and PR automation.
*   **`vectorService.js`**: Chunking and mathematical similarity search logic using Pinecone.
*   **`sandboxService.js`**: The OS-level wrapper around the `child_process` for secure iterative testing.
*   **`cronService.js`**: The automated 5-minute schedule heartbeat.
*   **`aiService.js`**: The HTTP multi-model parser handling prompt structuring.

*Built by the Quantum AI Code Agent system.*
