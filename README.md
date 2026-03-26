# GTM Skills for Claude Code

A collection of ready-to-use [Claude Code Skills](https://docs.anthropic.com/en/docs/claude-code/skills) for go-to-market teams. Drop them into your workflow and start researching leads, enriching contacts, and gathering prospect intel — all from your terminal.

Powered by [CompanyEnrich](https://companyenrich.com) APIs.

## Skills

| Skill | Description |
|-------|-------------|
| **Lead Research Agent** | Full-pipeline lead research by email — person lookup, company enrichment, workforce trends |

## Quick Start

### 1. Get a CompanyEnrich API key

Sign up at [companyenrich.com](https://companyenrich.com) and grab your API key.

### 2. Install a skill

Download the `.skill` file and install it in Claude Code:

```
/skill install lead-research-agent.skill
```

### 3. Use it

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

## What You Get

### Lead Research Agent

Given an email address, this skill calls three CompanyEnrich API endpoints and builds a structured report:

- **Person** — Name, title, seniority, department, location, LinkedIn
- **Company** — Description, categories, funding history (rounds, investors, amounts)
- **Workforce** — Department headcount breakdown, employee count, and trend analysis (flags departments with >15% headcount changes)

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI
- A [CompanyEnrich](https://companyenrich.com) API key

## License

MIT
