# Capstone IPO — IPO Prediction Platform

A full-stack platform for analyzing and predicting IPO outcomes. Users submit company and
offering details through a guided multi-step form, and the platform returns AI-assisted price
predictions and a risk analysis. Built as a capstone project.

This repo combines the two halves of the project:

- **`backend/`** — FastAPI REST API, backed by Appwrite Cloud (auth, database)
- **`frontend/`** — React + Vite single-page app

## Features

- **Multi-step IPO submission form** — company details, offering structure, and financials
  collected across a guided flow, then submitted as one workflow
- **AI-powered price predictions** — model-driven IPO price range estimates
- **Risk analysis** — structured risk scoring alongside each prediction
- **Prediction history** — past predictions tracked per user
- **User accounts** — registration and login with JWT-based auth
- **Company records** — CRUD for company data backing each analysis

## Tech stack

**Backend**
- FastAPI + Uvicorn
- Appwrite Cloud (users, database)
- Pydantic for request/response validation
- `python-jose` for JWT auth

**Frontend**
- React 19 + Vite
- Tailwind CSS
- React Hook Form + Zod for form state and validation
- Axios for API calls
- React Router for navigation
- Lucide icons

## Project structure

```
backend/
├── app/
│   ├── main.py              # FastAPI app entry, route registration
│   ├── config.py            # Appwrite env config
│   ├── auth/                # JWT auth helpers
│   ├── models/               # Pydantic schemas (user, company, IPO)
│   ├── routes/               # users, companies, ipo_routes, auth
│   └── services/              # Appwrite client + business logic per domain
├── create_collection.py            # One-off Appwrite collection setup
├── create_collections_complete.py  # Full schema seed script
└── requirements.txt

frontend/
├── src/
│   ├── pages/                # HomePage, LoginPage, RegisterPage, ResultsPage, NotFoundPage
│   ├── components/
│   │   ├── MultiStepForm.jsx       # The core IPO submission flow
│   │   ├── PriceChart.jsx          # Prediction visualization
│   │   ├── RiskMeter.jsx           # Risk score display
│   │   ├── CompanyList.jsx / CreateCompany.jsx
│   │   ├── SiteHeader.jsx / SiteFooter.jsx / Layout.jsx
│   │   └── ui/                     # Reusable primitives (Button, Card, Input, Form, ...)
│   └── services/api.js       # API client, points at the backend
└── package.json
```

## Getting started

### 1. Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env          # then fill in your Appwrite credentials
uvicorn app.main:app --reload
```

Runs at `http://localhost:8000`. Interactive docs at `http://localhost:8000/docs`.

You'll need an [Appwrite Cloud](https://cloud.appwrite.io) project with a database configured.
Required `.env` values: `APPWRITE_PROJECT_ID`, `APPWRITE_API_KEY`, `APPWRITE_DATABASE_ID`.

### 2. Frontend

```bash
cd frontend
npm install
npm run dev
```

Runs at `http://localhost:5173`, and expects the backend at `http://localhost:8000`
(configurable in `frontend/src/services/api.js`).

## API overview

All IPO-related endpoints are under `/ipo`:

| Endpoint | Description |
|---|---|
| `GET /ipo/health` | Health check |
| `POST /ipo/submit-multistep-form` | Submit the full multi-step IPO form |
| `GET /ipo/predictions/` | List predictions |
| `GET /ipo/risk-analysis/` | List risk analyses |
| `GET /ipo/users/{user_id}/history` | A user's prediction history |
| `GET /ipo/analysis/{user_id}/{prediction_id}` | Full analysis for one prediction |

User and company management live under `/users` and `/companies` respectively.

## Status

Core workflow is implemented end to end: form submission, prediction and risk-analysis
endpoints, user management, and a frontend wired to all of it. Live data requires a configured
Appwrite project — without one, the app still runs and renders, but database-backed requests
will fail until credentials are added.

## License

Not yet licensed — add a `LICENSE` file if you want this to be reusable by others (MIT is a
common default for portfolio projects).
