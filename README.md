# Stash — Personal Finance, Made Clear

Stash is a full-stack personal-finance app with a React Native (Expo) client and a FastAPI backend. It brings transactions, budgets, savings goals, recurring expenses, insights, CSV export, and an AI-assisted finance chat into one mobile experience.

> **Project status:** Active prototype. Do not use it as a financial, tax, or investment adviser.

## Features

- Track income and expenses, with categories, notes, and payment methods.
- Review spending trends and budget utilization.
- Manage savings goals and recurring expenses.
- Ask the AI assistant questions about your financial context.
- Export transaction data as CSV.

## Stack

| Area | Tools |
| --- | --- |
| Mobile | React Native, Expo, TypeScript, React Navigation |
| API | Python, FastAPI, SQLAlchemy, Alembic |
| Data | SQLite for local development; PostgreSQL is supported by configuration |
| AI | Gemini by default; an OpenAI provider is also configurable |

## Repository layout

```text
backend/   FastAPI application, migrations, tests, and environment template
mobile/    Expo / React Native application
docker-compose.yml  Optional local service configuration
```

## Run locally

### Backend

Requirements: Python 3.11 or newer. From the repository root:

```bash
cd backend
python -m venv .venv
# Linux/macOS
source .venv/bin/activate
# Windows PowerShell: .venv\Scripts\Activate.ps1
pip install -r requirements.txt
cp .env.example .env  # On Windows: copy .env.example .env
```

Edit `backend/.env` and set a strong `SECRET_KEY`, a local `DATABASE_URL`, and (if using AI) your provider API key. Never commit `.env` or production credentials. Run the API from `backend/`:

```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

The health endpoint is `http://localhost:8000/health`. Interactive API docs are available at `/docs` when `DEBUG=true`.

### Mobile app

In another terminal, from the repository root:

```bash
cd mobile
npm install
```

Set the API base URL in `mobile/src/constants/api.ts` to an address reachable from your device (for example, `http://10.0.2.2:8000` for the Android emulator), then start Expo:

```bash
npm start
```

Use the Expo CLI to open the app on a simulator, device, or web where supported.

## Configuration and privacy

Backend variables are documented in [`backend/.env.example`](./backend/.env.example). The mobile app communicates with the API; use test data during development and review authentication, authorization, CORS, database backups, and AI-provider data handling before any deployment. Do not use real personal financial data in an unreviewed instance.

## Tests

From `backend/` with the virtual environment active:

```bash
pytest
```

## License

The mobile subproject includes the [Expo MIT license](./mobile/LICENSE). Review its scope before treating it as a license for the entire repository.

## Maintainer

[Mayank Bohara](https://github.com/mayankbohara0-dev)
