# 🤖 AI Question Answering Chatbot

> Full-stack AI Chatbot built with FastAPI + React + PostgreSQL + Groq (Free LLM) + Docker + Prometheus + Grafana + Jenkins CI/CD

---

## 🏗️ Architecture

Browser (User)
↓ HTTP :80
Frontend (React + Nginx)
↓ /api/*
Backend (FastAPI)
↓                ↓
PostgreSQL          Groq AI API
(History)           (Free LLM)
Prometheus → scrapes /metrics
Grafana    → visualizes dashboards
Jenkins    → CI/CD pipeline

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18 + Vite + Nginx |
| Backend | FastAPI (Python 3.11) |
| Database | PostgreSQL 16 |
| AI Model | Groq LLaMA 3 (100% Free) |
| Monitoring | Prometheus + Grafana |
| CI/CD | Jenkins Pipeline |
| Container | Docker + Docker Compose |

---

## 📁 Project Structure

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    CI/CD PIPELINE (JENKINS)                     │
│                                                                 │
│  1.Code    2.Webhook   3.Checkout  4.Build   5.Push   6.Deploy │
│  Commit ──► Jenkins ──► Git ──────► & Test ──► DockerHub ──► ▼ │
└─────────────────────────────────────────────────────────────────┘
                                                        │
                                               ┌────────▼────────┐
                                               │ CONTAINER       │
                                               │ REGISTRY        │
                                               │ (Docker Hub)    │
                                               └────────┬────────┘
                                                        │
┌───────┐  HTTP/HTTPS  ┌─────────────────────────────────────────┐
│       │    :80/:443  │         DOCKER NETWORK: chatbot-net      │
│  USER ├─────────────►│                                          │
│Browser│              │  ┌──────────────────────────────────┐   │
└───────┘              │  │     NGINX (Reverse Proxy)        │   │
                       │  │  • SSL Termination               │   │
                       │  │  • Security Headers              │   │
                       │  │  • Gzip Compression              │   │
                       │  │  • Proxy /api → Backend          │   │
                       │  └────────┬──────────────┬──────────┘   │
                       │           │ Serve /       │ /api/*       │
                       │  ┌────────▼──────┐ ┌─────▼───────────┐ │
                       │  │   FRONTEND    │ │    BACKEND       │ │
                       │  │ React + Vite  │ │   FastAPI        │ │
                       │  │ Node.js/Nginx │ │   Python 3.11    │ │
                       │  │               │ │                  │ │
                       │  │ • Chat UI     │ │ • REST API       │ │
                       │  │ • API Calls   │ │ • Business Logic │ │
                       │  │ • Static      │ │ • Groq Integration│ │
                       │  │   Assets      │ │ • Prometheus     │ │
                       │  └───────────────┘ │   Metrics        │ │
                       │                    └──────┬──────┬────┘ │
                       │                           │      │      │
                       │              SQL Queries  │      │HTTPS │
                       │                    ┌──────▼──┐ ┌─▼────┐│
                       │                    │DATABASE │ │GROQ  ││
                       │                    │PostgreSQL│ │ API  ││
                       │                    │  :5432  │ │(Free)││
                       │                    │         │ │LLaMA3││
                       │                    │• Conver-│ └──────┘│
                       │                    │  sations│         │
                       │                    │• Messages│        │
                       │                    │• History│         │
                       │                    └─────────┘         │
                       │                                         │
                       │  ┌──────────────┐   ┌───────────────┐  │
                       │  │  PROMETHEUS  │──►│    GRAFANA    │  │
                       │  │    :9090     │   │    :3001      │  │
                       │  │              │   │               │  │
                       │  │ Scrapes      │   │ • Dashboards  │  │
                       │  │ /metrics     │   │ • Graphs      │  │
                       │  │ every 15s    │   │ • Alerts      │  │
                       │  └──────────────┘   └───────────────┘  │
                       └─────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                         DATA FLOW                               │
│                                                                 │
│  User ──► Nginx :80 ──► Frontend (React)                       │
│                    └──► /api/* ──► Backend (FastAPI)           │
│                                       ├──► PostgreSQL (History)│
│                                       └──► Groq API (AI Reply) │
│                                                                 │
│  Prometheus ──► scrapes /metrics ──► Grafana (Dashboard)       │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                    DOCKER SERVICES                              │
│                                                                 │
│  chatbot-postgres   → PostgreSQL 16      (port 5432)           │
│  chatbot-backend    → FastAPI            (port 8000)           │
│  chatbot-frontend   → React + Nginx      (port 80)             │
│  chatbot-prometheus → Prometheus         (port 9090)           │
│  chatbot-grafana    → Grafana            (port 3001)           │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🚀 Quick Start

### Step 1 — Free Groq API Key lo

https://console.groq.com pe jaao
Sign Up karo (bilkul free, card nahi chahiye)
API Keys → Create API Key
Key copy karo (gsk_ se shuru hogi)

### Step 2 — Environment setup karo
```bash
cp backend/.env.example backend/.env
nano backend/.env
# GROQ_API_KEY=gsk_tumhari_key_yahan_paste_karo
```

### Step 3 — Docker se run karo
```bash
docker compose up --build
```

---

## 🌐 Access URLs

| Service | URL | Login |
|---------|-----|-------|
| Chatbot App | http://localhost | — |
| API Docs | http://localhost:8000/docs | — |
| Health Check | http://localhost/health | — |
| Prometheus | http://localhost:9090 | — |
| Grafana | http://localhost:3001 | admin / admin |

---

## ✅ Features

- 💬 AI Chat — Groq LLaMA 3 powered (100% free)
- 🧠 Conversation history — PostgreSQL mein store hoti hai
- ⚡ Session management — browser localStorage se
- 📊 Real-time monitoring — Prometheus + Grafana
- 🐳 One command setup — docker compose up --build
- 🔒 Secure — API keys environment variables mein
- 🔄 CI/CD — Jenkins pipeline included

---

## 🔄 CI/CD Pipeline (Jenkins)

---

## 📊 Monitoring Setup

### Prometheus
- URL: http://localhost:9090
- FastAPI metrics scrape karta hai `/metrics` se
- Query example: `http_requests_total`

### Grafana
- URL: http://localhost:3001 (admin/admin)
- Prometheus data source add karo
- URL: `http://chatbot-prometheus:9090`

---

## 🐳 Docker Commands

```bash
# Start all services
docker compose up --build -d

# View logs
docker compose logs -f backend

# Container status
docker ps

# Stop all
docker compose down

# Stop + delete data
docker compose down -v
```

---

## 🆓 Free Groq Models

`.env` mein `GROQ_MODEL` change karo:

| Model | Speed | Use |
|-------|-------|-----|
| llama-3.3-70b-versatile | Fast | Best quality (recommended) |
| llama3-70b-8192 | Fast | Good quality |
| mixtral-8x7b-32768 | Fast | Long context |

---

## 🛠️ API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /health | Health check |
| GET | /metrics | Prometheus metrics |
| GET | /docs | Swagger API docs |
| POST | /api/chat | AI ko message bhejo |
| GET | /api/conversations/{id} | Chat history lo |
| DELETE | /api/conversations/{id} | Conversation delete karo |

---

## 🔐 Environment Variables

```env
GROQ_API_KEY=gsk_...          # Groq API key (required)
GROQ_MODEL=llama-3.3-70b-versatile
DB_HOST=postgres
DB_PORT=5432
DB_NAME=appdb
DB_USER=appuser
DB_PASSWORD=apppassword
CORS_ORIGINS=http://localhost
```

---

## 👨‍💻 Developer

**Sonu Kumar Jha**  
Stack: FastAPI + React + Docker + Groq + Prometheus + Grafana + Jenkins
