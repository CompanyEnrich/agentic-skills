# Lead Research Agent

Full-pipeline lead research by email — person lookup, company enrichment, and workforce trend analysis. Powered by [CompanyEnrich](https://companyenrich.com) APIs.

## What It Does

Given an email address, this skill calls three CompanyEnrich API endpoints and builds a structured report:

- **Person** — Name, title, seniority, department, location, LinkedIn
- **Company** — Description, categories, funding history (rounds, investors, amounts)
- **Workforce** — Department headcount breakdown, employee count, and trend analysis (flags departments with >15% headcount changes)

## Install

```
/skill install lead-research-agent.skill
```

## Usage

Just ask Claude to research a lead:

```
Research john@acme.com
```

```
Who is sarah@startup.io?
```

```
Enrich this contact: mike@bigcorp.com
```

The skill handles the rest — it runs a reverse email lookup, enriches the company, pulls workforce data, and presents a clean report.

## API Key Setup

On first run, Claude will ask for your [CompanyEnrich](https://companyenrich.com) API key and save it to memory so you only need to provide it once.

## API Endpoints Used

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/people/lookup` | POST | Reverse email lookup — person details, role, seniority |
| `/companies/enrich` | GET | Company profile, categories, funding rounds |
| `/companies/workforce` | GET | Department headcount, employee count, historical trends |
