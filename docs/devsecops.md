# DevSecOps

**Owner:** Security / DevSecOps · **Backend choice:** Python 3.14 (FastAPI). The C# starter was removed to keep one language for the API and tests.

## Pipeline

`.github/workflows/devsecops.yml` runs on every push and PR to `main`/`dev`:

| Stage | Tool | Scans | Blocks the pipeline? | Evidence (artifact) |
|---|---|---|---|---|
| Build | `compileall` | App source | Yes, on error | job log |
| Test | pytest + pytest-cov | `tests/python` | Yes, on any failure | `test-results` |
| SAST | Bandit | `api/python/app` | Yes, on **MEDIUM+** severity with medium+ confidence. Medium because SQL injection (B608) is rated Medium | `sast-bandit` |
| SAST | CodeQL | Python | Shows in Security tab; public repos only | Security → Code scanning |
| SCA | pip-audit | `api/python/requirements.txt` (incl. transitive) | Yes, on **any** known vulnerability | `sca-pip-audit` |
| DAST | OWASP ZAP API scan | Running API, via `/openapi.json` (exercises `POST /calculate`) | No (report only in Sprint 1) | `dast-zap` |
| Deploy gate | — | — | Runs only if all blocking stages pass | job log |

**Team to agree and record here:** when ZAP becomes blocking (proposal: from Sprint 2, fail on High via a rules file + `fail_action: true`), and how medium/low findings are triaged (proposal: an issue per finding, fix or justify within the sprint).

## Findings log

Record every finding: tool, ID, component/version, severity, decision, fix, retest.

| # | Date | Tool | Finding | Severity | Decision / remediation | Retest |
|---|---|---|---|---|---|---|
| 1 | | pip-audit | Supplied starter pinned `fastapi==0.115.6` → `starlette 0.41.3` with 14 known advisories (e.g. PYSEC-2026-1941, fixed in 0.47.2) | see report | Upgraded to `fastapi==0.162.5` (current starlette) | pip-audit clean |
| 2 | | Bandit | _Deliberate finding: e.g. SQL built with an f-string (B608, Medium) or `subprocess(..., shell=True)` (B602, High)_ | | | |

## Evidence checklist (save to `docs/evidence/`)

- [ ] Successful build
- [ ] Unit-test results
- [ ] SAST results
- [ ] SCA results
- [ ] DAST results
- [ ] Deliberately generated security finding (red pipeline)
- [ ] Remediation of the finding (green pipeline)

## Secrets

No secrets in the repo. Local config lives in `.env` (gitignored, template in `.env.example`); CI uses GitHub Actions secrets. Enable **Settings → Code security → Secret scanning / Push protection** if available. Azure Key Vault from Sprint 2.
