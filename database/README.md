# Database runbook

**Owner:** Infra / Data · **Status:** TODO

Document how anyone can stand up the database and API from scratch:

1. **SQL Server:** which one (course-provided / Docker `mcr.microsoft.com/mssql/server` / Azure SQL), how to get access
2. **Create the database:** `CREATE DATABASE CarbonAdvisor;`
3. **Run scripts:** e.g. `sqlcmd -S <server> -d CarbonAdvisor -i database/schema.sql` then `seed.sql`
4. **Verify:** T-SQL queries that prove the seed worked (save screenshots to `docs/evidence/`)
5. **Configure the API:** copy `.env.example` to `.env` and set the values; never commit `.env`
6. **Run the API:** see the root README
