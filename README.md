# 🌌 AntigravityAI

> **Production Autonomous PC Troubleshooting & Diagnostic Agent** with Advanced CSS Grid Mission Control, Multi-LLM Orchestration (OpenAI GPT-4o & Google Gemini), Real-Time Policy Enforcement, and Instant Cloud Deployment.

---

## 🚀 Key Highlights

- **Seamless Synchronization**: Zero-asynchronicity connection between React frontend and FastAPI backend with active health beacons, latency telemetry, and resilient timeout fallbacks.
- **Advanced Mission Control UI**: 3-column CSS Grid responsive architecture featuring:
  - **Left Panel**: Security Policy Enforcement Matrix & Capability Tags
  - **Center Hub**: Neural Diagnostic Chat Terminal with animated waveform visualizer & prompt presets
  - **Right Panel**: Whitelisted Diagnostic Action Deck (`list_files`, `read_file`) & Persistent Memory Explorer
- **Multi-LLM Integration**: Native support for OpenAI `gpt-4o` and Google Gemini `gemini-2.5-flash` with graceful fallback handling.
- **Enterprise Governance**: Deterministic policy enforcement matrix (Read allowed, Deletions strictly locked) derived from `agent.json` and `docs/`.
- **1-Click Production Deployment**: Pre-configured for **Railway** (`railway.json`, `Procfile`) and **Render** (`render.yaml`, `Dockerfile`).

---

## 📂 Project Architecture

```
AntigravityAI/
├── agent.json              # Master project manifest
├── Dockerfile              # Multi-stage production container (Node + Python)
├── render.yaml             # Render Blueprint configuration
├── railway.json            # Railway deployment configuration
├── Procfile                # PaaS process manager specification
├── DEPLOYMENT.md           # Step-by-step Railway & Render guide
├── n8n-workflow.json       # Slack + n8n automation pipeline
│
├── backend/                # FastAPI Microservice
│   ├── main.py             # Server entrypoint with CORS & static SPA hosting
│   ├── agent.py            # Governance context aggregator
│   ├── memory_manager.py   # Persistent JSON memory store
│   ├── policy_engine.py    # Action authorization engine
│   ├── tools.py            # Diagnostic tools (list_files, read_file)
│   └── requirements.txt    # Python dependencies
│
├── frontend/               # React 19 + Vite Frontend
│   ├── src/
│   │   ├── App.jsx         # Mission Control Dashboard (Advanced Grid)
│   │   ├── App.css         # Cyberpunk Grid layout & animated graphics
│   │   ├── index.css       # Global resets & CSS custom properties
│   │   └── api.js          # Synchronized API client & health prober
│   └── dist/               # Pre-compiled production bundle
│
├── docs/                   # Governance & Brain Rules
│   ├── agents.md           # Identity & objectives
│   ├── instructions.txt    # Step-by-step instructions
│   ├── constraints.md      # Safety boundaries
│   ├── policies.md         # Operational policy matrix
│   └── capabilities.json   # Machine-readable permissions
│
├── memory/
│   └── memory.json         # Persistent session summaries & known issues
├── config/
│   └── .env                # API keys & model configuration
└── logs/                   # System activity logs
```

---

## ⚡ Quick Start (Local)

### 1. Configure Environment
Set your API keys in `config/.env`:
```ini
OPENAI_API_KEY=your_openai_key
# OR
GOOGLE_API_KEY=your_gemini_key
OPENAI_MODEL=gpt-4o
```

### 2. Start Unified Server
```powershell
python -m uvicorn backend.main:app --host 0.0.0.0 --port 8000
```
Open **`http://localhost:8000`** in your browser to experience the full Mission Control Dashboard!

---

## 🚢 Cloud Deployment (Railway & Render)

See the full [DEPLOYMENT.md](file:///C:/Users/Administrator/.gemini/antigravity/scratch/AntigravityAI/DEPLOYMENT.md) for step-by-step instructions:
- **Railway**: Connect repo → Auto-builds from `Dockerfile` → Set `OPENAI_API_KEY` → Live in 60s!
- **Render**: Connect repo → Select Blueprint `render.yaml` → Set `OPENAI_API_KEY` → Deployed!
