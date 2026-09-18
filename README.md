# Capstone IPO — Prediction Platform

Full-stack IPO analysis platform: AI-assisted IPO predictions, risk analysis, and a multi-step
submission workflow. This repo combines the two halves of the project into one place:

- **`backend/`** — FastAPI backend backed by Appwrite Cloud. Handles users, companies, IPO
  predictions, and risk analysis.
- **`frontend/`** — React + Vite frontend that talks to the backend's `/ipo/*` endpoints.

## Running it locally

### 1. Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env       # then fill in your Appwrite project credentials
uvicorn app.main:app --reload
```

Backend runs at `http://localhost:8000`. Interactive API docs at `http://localhost:8000/docs`.

You'll need an [Appwrite Cloud](https://cloud.appwrite.io) project with a database configured —
the backend won't start without valid `APPWRITE_PROJECT_ID`, `APPWRITE_API_KEY`, and
`APPWRITE_DATABASE_ID` values in `.env`.

### 2. Frontend

```bash
cd frontend
npm install
npm run dev
```

Frontend runs at `http://localhost:5173` and expects the backend at `http://localhost:8000`
(see `frontend/src/services/api.js` if you need to point it elsewhere).

## Tech stack

- **Backend:** FastAPI, Appwrite (users, database), Pydantic, JWT auth
- **Frontend:** React 19, Vite, Tailwind CSS, React Hook Form, Zod, Axios

## Status

Core workflow is functional: form submission, prediction endpoints, risk analysis, and user
management routes are implemented and the frontend is wired to the backend's `/ipo/*` API.
