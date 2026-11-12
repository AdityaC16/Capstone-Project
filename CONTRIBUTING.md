# Contributing

## Workflow

1. Pick an issue from the board that meets the [Definition of Ready](docs/definition-of-ready.md) and assign yourself.
2. Branch from `dev`:
   ```bash
   git switch dev && git pull
   git switch -c feature/<issue#>-short-name     # or bugfix/<issue#>-short-name
   ```
3. Commit little and often with clear messages, e.g. `Add validation for spending amount (#12)`.
4. Push and open a PR **into `dev`** using the PR template. Link the issue (`Closes #12`).
5. Pipeline must be green and 1 teammate must approve. The reviewer checks code, tests and security.
6. Squash-merge, delete the branch, move the card.

`dev` is merged into `main` at the end of each sprint by the Scrum Master.

## Rules

- **No secrets in code.** Use `.env` locally (gitignored) and GitHub Secrets in CI. If a secret is ever pushed, tell the Security owner straight away and rotate it, because deleting the commit is not enough.
- **Synthetic data only.**
- **Parameterised SQL only.** Never build queries with f-strings or string concatenation.
- **Validate all input** at the API boundary (Pydantic models).
- **Add tests with your change.** Bug fixes come with a test that would have caught the bug.
- **Avoid new dependencies** unless needed. Pin exact versions in `requirements.txt` and say why in the PR.
- **AI-generated code:** you must read it, understand it, test it and scan it before opening the PR. Note in the PR that AI was used. Never paste secrets or customer data into AI tools.

## Stuck?

If you've been blocked for 30 minutes, post in the team channel. Someone swarms on it with you.
