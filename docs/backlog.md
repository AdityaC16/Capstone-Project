# Product backlog

**Owner:** Product Owner (with Scrum Master). Live board: GitHub Projects. This file is the summary.

Priority: **M** = MVP must-have, **S** = stretch (only after MVP is done and signed off).

## Epics (from the brief)

| Epic | Sprint | Priority |
|---|---|---|
| E1 Foundations: repo, API skeleton, SQL schema/seed, DevSecOps pipeline | 1 | M |
| E2 Submit monthly spending (stored securely) | 1–2 | M |
| E3 Carbon calculation from emissions factors | 2 | M |
| E4 Category insights + recommendations + potential savings | 3 | M |
| E5 Progress over time (trends) | 3 | M |
| E6 Sustainability challenges | 3–4 | M |
| E7 Dashboard / customer UI | 3–4 | M |
| E8 Deployment, end-to-end + security testing, docs, showcase | 4 | M |
| E9 AI-assisted recommendations, predictive savings, auth/RBAC, Key Vault, Terraform | any | S |

## Sprint 1 stories

| # | Story | Owner | Status |
|---|---|---|---|
| | As a team, we have a repo with branches, protection and a board so we can collaborate safely | Scrum Master | |
| | As a customer, I can POST my spending to `/calculate` and get a valid response | Backend | |
| | As a team, the API contract is documented so frontend/backend/tests can work in parallel | API & quality | |
| | As a team, automated tests prove the API builds, starts, accepts valid input and rejects invalid input | API & quality | |
| | As a team, the database has Categories, EmissionsFactors (source, version, effective date) and Assumptions, seeded for Travel/Food/Utilities | Infra | |
| | As a team, every push runs Build → Test → SAST → SCA → DAST with evidence retained | Security | |
| | As a team, we can show a security finding being detected and fixed | Security | |
| | As a customer, my journey is mapped and wireframed | Frontend / PO | |
