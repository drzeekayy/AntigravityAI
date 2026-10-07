# 🚀 AntigravityAI Production Deployment Guide (Railway & Render)

AntigravityAI is built with a decoupled architecture (FastAPI backend + Vite React frontend) that can be deployed in two modes:

1. **Unified Container (Recommended)**: A single multi-stage Docker container builds the React frontend and serves both the API and the SPA from FastAPI on a single port (`$PORT`). **Zero CORS issues, single domain, easiest setup.**
2. **Decoupled Services**: Deploy FastAPI on Railway/Render Web Service and React on Render Static Site or Vercel. Fully supported via configured `CORSMiddleware`.

---

## Option 1: Deploy on Railway (Fastest & 1-Click)

### Step 1: Push Repository to GitHub
Ensure your repository contains the root `Dockerfile`, `railway.json`, `agent.json`, `backend/`, and `frontend/`.

```bash
git add .
git commit -m "feat: production mission control & deployment configs"
git push origin main
```

### Step 2: Create Railway Project
1. Go to [railway.app](https://railway.app) and sign in.
2. Click **New Project** → **Deploy from GitHub repo**.
3. Select your `AntigravityAI` repository.
4. Railway will automatically detect the root `Dockerfile` and `railway.json`.

### Step 3: Configure Environment Variables
Under the **Variables** tab of your service, add:
- `OPENAI_API_KEY`: `your_openai_api_key_here` (or leave empty if using Gemini)
- `GOOGLE_API_KEY`: `your_gemini_api_key_here` (optional, for Gemini fallback)
- `OPENAI_MODEL`: `gpt-4o` (or `gemini-2.5-flash`)
- `PORT`: (Managed automatically by Railway, defaults to `8000`)

### Step 4: Generate Public Domain
1. In your service settings, navigate to **Networking** → click **Generate Domain**.
2. Railway will give you a public URL (e.g., `https://antigravity-ai-production.up.railway.app`).
3. Visit the URL in your browser to open the **Mission Control Dashboard**.
4. Test health probe at `https://<your-domain>/health`.

---

## Option 2: Deploy on Render

### Method A: Blueprint Deployment (render.yaml)
1. Sign in to [render.com](https://render.com).
2. Click **New +** → **Blueprint**.
3. Connect your GitHub repository.
4. Render detects `render.yaml` and sets up the Docker Web Service automatically.
5. In the prompts, enter your `OPENAI_API_KEY` or `GOOGLE_API_KEY`.
6. Click **Apply**.

### Method B: Manual Web Service Setup
1. Click **New +** → **Web Service**.
2. Connect your GitHub repository.
3. Configure the following:
   - **Name**: `antigravity-ai`
   - **Runtime**: `Docker`
   - **Dockerfile Path**: `./Dockerfile`
   - **Instance Type**: `Free`
   - **Health Check Path**: `/health`
4. Under **Environment Variables**, add:
   - `OPENAI_API_KEY`: `your_openai_api_key`
   - `GOOGLE_API_KEY`: `your_gemini_api_key`
   - `OPENAI_MODEL`: `gpt-4o`
5. Click **Deploy Web Service**.
6. When deployment finishes, open your Render `.onrender.com` URL in the browser!

---

## Verifying Production Readiness

| Checkpoint | Target | Expected Result |
| :--- | :--- | :--- |
| **Health Probe** | `GET /health` | `{"agent": "AntigravityAI", "status": "online", "model": "...", ...}` |
| **Mission Control UI** | `GET /` | Returns the glowing Cyberpunk Dashboard |
| **Policy Enforcement** | `GET /policies` | Returns JSON policy matrix and capabilities |
| **Memory Store** | `GET /memory` | Returns session history and catalogued issues |
| **Neural Inference** | `POST /ask` | Sends query and returns structured agent reply |
| **Tool Deck** | `POST /action` | Executes safe inspection (`list_files`, `read_file`) |

---

## Local Development (Testing Before Deploying)

If you wish to test locally before pushing to production:

### 1. Start Backend (Port 8000)
```powershell
python -m uvicorn backend.main:app --host 0.0.0.0 --port 8000
```

### 2. Start Frontend (Port 5173 with Vite HMR)
```powershell
cd frontend
npm run dev
```

Open `http://localhost:5173` for hot-reloading development, or `http://localhost:8000` to preview the production static bundle!
