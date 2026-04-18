# Proctoring AI

AI-assisted online exam proctoring system with a FastAPI backend, a student exam frontend, an admin dashboard, PostgreSQL, Redis, and MinIO evidence storage.

The system supports student authentication, face verification, live webcam proctoring, violation logging, exam creation, live admin monitoring, result summaries, and evidence review.

## Project Structure

```text
.
|-- Proctoring-AI-BE-M4/Proctoring-AI-BE-M4/      # FastAPI backend and AI detection services
|-- Proctoring-AI-FE-M4/Proctoring-AI-FE-M4/      # Student-facing React/Vite app
|-- Proctoring-AI-Admin/                          # Admin React/Vite dashboard
|-- docker-compose.yml                            # Backend, PostgreSQL, Redis, MinIO, Adminer
|-- .env.example                                  # Root local development environment example
|-- PROJECT_UNDERSTANDING_REPORT.docx             # Project report
|-- DEPLOYMENT_CHECKLIST.md                       # Deployment notes
|-- PROCTORING_POLICY_MAP.md                      # Proctoring policy reference
```

## Main Features

- Student login with password and face verification
- Guided face enrollment and liveness challenge flow
- Real-time exam monitoring over WebSocket
- Face absence, gaze, hand, phone, and multiple-person detection
- Screen recording/session capture support
- Admin exam creation and eligible student management
- Live admin monitoring dashboard
- Evidence vault and exam result summaries
- PostgreSQL persistence, Redis session support, and MinIO evidence storage
- LTI endpoint support for LMS integration

## Tech Stack

- Backend: FastAPI, SQLAlchemy, Alembic, Gunicorn, Uvicorn
- AI/CV: YOLOv8, MediaPipe, OpenCV, TensorFlow/Keras, DeepFace-related tooling
- Frontend: React 18, Vite, Redux Toolkit, React Router
- Admin: React 18, Vite, TypeScript, Radix UI, Recharts
- Infrastructure: Docker Compose, PostgreSQL, Redis, MinIO, Adminer

## Prerequisites

- Git and Git LFS
- Docker Desktop
- Node.js 18 or newer
- Python 3.9 if running the backend outside Docker

The backend model file `yolov8n.pt` is stored with Git LFS.

```powershell
git lfs install
git lfs pull
```

## Quick Start

### 1. Configure the root environment

From the repository root:

```powershell
Copy-Item .env.example .env
```

Update secrets in `.env` before using the project outside local development.

### 2. Start backend services

```powershell
docker compose up --build
```

This starts:

- Backend API: `http://localhost:8080`
- API docs: `http://localhost:8080/docs`
- PostgreSQL: `localhost:5434`
- Redis: `localhost:6379`
- MinIO console: `http://localhost:9001`
- Adminer: `http://localhost:8081`

### 3. Start the student frontend

```powershell
Set-Location Proctoring-AI-FE-M4/Proctoring-AI-FE-M4
npm install
@"
VITE_API_URL=http://localhost:8080
VITE_WS_URL=ws://localhost:8080/ws
VITE_ADMIN_URL=http://localhost:5173
"@ | Set-Content .env
npm run dev
```

Student app: `http://localhost:5174`

### 4. Start the admin dashboard

Open another terminal from the repository root:

```powershell
Set-Location Proctoring-AI-Admin
npm install
@"
VITE_API_URL=http://localhost:8080/api/v1/
VITE_WS_URL=ws://localhost:8080/ws
"@ | Set-Content .env
npm run dev
```

Admin app: `http://localhost:5173`

## Default Local Configuration

The root `.env.example` enables local service wiring for Docker Compose. It also includes optional seed values:

```text
SEED_DEFAULT_USERS=true
SEED_ADMIN_EMAIL=admin@example.com
SEED_ADMIN_PASSWORD=change_me_for_real_deployment
```

Change these values before any shared, hosted, or production deployment.

## Common Commands

### Backend

```powershell
Set-Location Proctoring-AI-BE-M4/Proctoring-AI-BE-M4
pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 8080 --reload
```

### Student Frontend

```powershell
Set-Location Proctoring-AI-FE-M4/Proctoring-AI-FE-M4
npm run dev
npm run build
npm run lint
```

### Admin Dashboard

```powershell
Set-Location Proctoring-AI-Admin
npm run dev
npm run build
```

### Docker

```powershell
docker compose up --build
docker compose down
docker compose logs -f backend
```

## API Overview

Primary backend routes are mounted under `/api/v1`:

- `/api/v1/auth` - authentication, password login, face login, enrollment, profile
- `/api/v1/exam` - exam lifecycle, submissions, summaries, admin live data
- `/api/v1/settings` - proctoring and application settings
- `/api/v1/observability` - health and metrics endpoints
- `/api/v1/lti` - LMS/LTI integration endpoints
- `/ws/{user_id}` - student live proctoring WebSocket
- `/ws/admin/live` - admin live monitoring WebSocket

A Postman collection is available at:

```text
Proctoring-AI-BE-M4/Proctoring-AI-BE-M4/postman_collection/Proctoring AI - Sharath.postman_collection.json
```

## Notes for Deployment

- Replace all local secrets in `.env` and nested app `.env` files.
- Use HTTPS/WSS URLs for hosted frontend and backend deployments.
- Configure persistent volumes or managed storage for PostgreSQL and MinIO.
- Keep `yolov8n.pt` available through Git LFS or provide the model during deployment.
- Review `DEPLOYMENT_CHECKLIST.md` before publishing.

## Documentation

- `PROJECT_UNDERSTANDING_REPORT.docx` - full project explanation
- `LECTURER_HANDOFF.md` - handoff notes
- `PROCTORING_POLICY_MAP.md` - proctoring behavior and policy mapping
- `DEPLOYMENT_CHECKLIST.md` - deployment readiness checklist

