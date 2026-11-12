# Personal Carbon Footprint & Savings Advisor

Nationwide TDP 2026 Capstone. A customer-facing prototype that turns monthly spending into an estimated carbon footprint, then gives recommendations that cut both carbon and cost.

> All data in this repository is **synthetic**. Never add real customer information or secrets.

## Team

| Role | Name | Owns |
|---|---|---|
| Scrum Master | _tbc_ | Board, ceremonies, repo admin, DoR/DoD, reflection, showcase |
| Frontend / Product Owner (Sprint 1) | _tbc_ | User stories, customer journey, wireframes, UI |
| Backend | _tbc_ | FastAPI app, validation, business logic, carbon engine |
| Infra / Data | _tbc_ | SQL Server, `database/` schema + seed, runbook, deployment |
| Security / DevSecOps | _tbc_ | `.github/workflows/devsecops.yml`, scans, evidence |
| API, quality & cloud | _tbc_ | API contract, test suite, Azure, AI stretch |

## Tech stack

- **Python 3.14** with FastAPI + Uvicorn (backend choice: Python, see `docs/devsecops.md`)
- **pytest** + pytest-cov for automated tests
- **SQL Server / T-SQL** for spending and emissions data (`database/`)
- **GitHub Actions** pipeline: Build → Test → SAST (Bandit, CodeQL) → SCA (pip-audit) → DAST (OWASP ZAP) → Deploy gate

## Repository layout

```
api/python/app/        FastAPI application
api/python/            requirements.txt (runtime) and requirements-dev.txt (dev/CI)
tests/python/          pytest tests
database/              schema.sql, seed.sql, README.md (runbook)
frontend/              customer UI (from Sprint 2/3)
test-data/             synthetic spending datasets
docs/                  backlog, DoR, DoD, API contract, DevSecOps, reflections, evidence/
.github/workflows/     devsecops.yml
```

## Getting started

```bash
git clone <repo-url>
cd <repo>
python -m venv .venv
# Windows (PowerShell):  .venv\Scripts\Activate.ps1
# macOS/Linux:           source .venv/bin/activate
pip install -r api/python/requirements-dev.txt
cp .env.example .env        # then fill in your local DB details (never commit .env)
```

Run the API (from `api/python`):

```bash
cd api/python
uvicorn app.main:app --reload
```

- Swagger UI: http://127.0.0.1:8000/docs
- Health check: http://127.0.0.1:8000/health

Run the tests (from the repo root):

```bash
pytest
```

Run the security scans locally, the same way the pipeline does:

```bash
bandit -r api/python/app                       # SAST
pip-audit -r api/python/requirements.txt       # SCA
```

## API

| Method | Path | Purpose |
|---|---|---|
| GET | `/health` | Liveness check |
| POST | `/calculate` | Submit spending, get carbon estimate (mock until Sprint 2) |

Full request/response contract: [`docs/api-contract.md`](docs/api-contract.md).

## How we work

- Branches: `main` (release) ← `dev` (integration) ← `feature/<issue#>-short-name` / `bugfix/<issue#>-short-name`
- Every change goes through a pull request into `dev`: 1 approval + green pipeline
- `dev` → `main` at the end of each sprint
- See [CONTRIBUTING.md](CONTRIBUTING.md), [Definition of Ready](docs/definition-of-ready.md), [Definition of Done](docs/definition-of-done.md)

## Sprints

1. **Setup & first MVP:** repo, API skeleton, SQL schema/seed, DevSecOps pipeline
2. **Carbon calculation:** emissions factors, SQL integration, calculation engine
3. **Insights & recommendations:** trends, category analysis, savings, dashboard
4. **Final MVP & showcase:** end-to-end + security testing, deployment, docs
