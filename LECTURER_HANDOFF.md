# Lecturer Handoff

## What This Project Contains

- `Proctoring-AI-BE-M4/Proctoring-AI-BE-M4`: FastAPI backend
- `Proctoring-AI-FE-M4/Proctoring-AI-FE-M4`: student frontend
- `Proctoring-AI-Admin`: admin frontend
- `docker-compose.yml`: backend services launcher
- `.env`: root Docker and backend configuration

## What To Share

Give your lecturer the full project folder as a `.zip`, but make sure these are included:

- `.env` at the repo root
- `docker-compose.yml`
- `Proctoring-AI-BE-M4`
- `Proctoring-AI-FE-M4`
- `Proctoring-AI-Admin`

They do not need:

- `.git`
- `.venv`
- log files like `*.log`, `backend_logs.txt`
- `node_modules` folders if present

## Recommended Software

Use `Visual Studio Code`, not full Visual Studio.

Install:

- Visual Studio Code
- Docker Desktop
- Node.js 18+ or 20 LTS
- GitHub Copilot extension in VS Code if they want guided setup

## Easiest Way To Run

Recommended setup:

- Run the backend with Docker
- Run both frontends locally with Node.js

Expected local URLs:

- Backend API: `http://localhost:8080`
- Backend docs: `http://localhost:8080/docs`
- Student frontend: `http://localhost:5174`
- Admin frontend: `http://localhost:5173`

## Manual Run Steps

Open the project root in VS Code, then open the built-in terminal.

### 1. Start backend services

From the repo root:

```powershell
docker compose up --build -d
docker ps
```

### 2. Start admin frontend

Open a new terminal:

```powershell
cd Proctoring-AI-Admin
npm.cmd install
npm.cmd run dev
```

### 3. Start student frontend

Open another new terminal:

```powershell
cd Proctoring-AI-FE-M4\Proctoring-AI-FE-M4
npm.cmd install
npm.cmd run dev
```

## Notes

- The root `.env` file is required for `docker compose`.
- The frontend `.env` files are already inside:
  - `Proctoring-AI-Admin/.env`
  - `Proctoring-AI-FE-M4/Proctoring-AI-FE-M4/.env`
- If PowerShell says `npm.ps1 cannot be loaded`, use `npm.cmd` exactly as shown above.
- Backend user seeding depends on values in the root `.env`. Share the login credentials separately if needed.

## Copilot Prompt

Tell your lecturer to:

1. Open `Visual Studio Code`
2. Open this project folder
3. Open GitHub Copilot Chat on the left sidebar
4. Paste this prompt:

```text
This is a multi-part project with a FastAPI backend, a student frontend, and an admin frontend.

Please analyze this workspace and help me install and run it on my Windows laptop without changing any code.

Read these files first:
- docker-compose.yml
- .env
- run_all.ps1
- Proctoring-AI-BE-M4/Proctoring-AI-BE-M4/README.md
- Proctoring-AI-BE-M4/Proctoring-AI-BE-M4/requirements.txt
- Proctoring-AI-Admin/package.json
- Proctoring-AI-Admin/.env
- Proctoring-AI-FE-M4/Proctoring-AI-FE-M4/package.json
- Proctoring-AI-FE-M4/Proctoring-AI-FE-M4/.env

Then do the following:
1. Tell me the required software I must install first.
2. Give me the exact terminal commands to start the backend with Docker from the repo root.
3. Give me the exact terminal commands to install and run the admin frontend.
4. Give me the exact terminal commands to install and run the student frontend.
5. Assume I am using PowerShell on Windows. If npm.ps1 is blocked, use npm.cmd.
6. Do not modify source code unless I ask.
7. At the end, show me the URLs I should open in the browser:
   - backend API
   - backend Swagger docs
   - admin frontend
   - student frontend
8. Give me short troubleshooting help for:
   - Docker Desktop not running
   - port already in use
   - missing .env file
   - frontend not connecting to backend
```

## Short Message You Can Send With The Zip

```text
Please use Visual Studio Code for this project. Open the folder in VS Code, open GitHub Copilot Chat on the left side, and paste the setup prompt from LECTURER_HANDOFF.md. The easiest setup is Docker Desktop for the backend and npm for the two frontends.
```
