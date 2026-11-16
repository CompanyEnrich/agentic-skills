---
name: lead-research-agent
description: >
  Automated lead research agent powered by CompanyEnrich APIs. Use this skill whenever the user
  wants to research a lead by email, enrich a contact, look up a lead, run lead research, or
  get intel on a prospect. Also trigger when the user says "research this lead," "look up
  this email," "enrich this contact," "who is [email]," "run lead intel on," or provides an
  email address and wants company/person info gathered. If a lead email is mentioned and research
  or enrichment is implied, use this skill. This skill handles the full pipeline: reverse email
  lookup, company enrichment, workforce data with trend analysis. Results are displayed directly
  in chat.
---

# Lead Research Agent

Research any lead by email using CompanyEnrich APIs. Extract the domain from the email and run
3 API calls, then display a clean report in chat.

## Config

Read the CompanyEnrich API key from the `COMPANYENRICH_API_KEY` environment variable.

If the variable is not set, stop and tell the user:

> "I need a CompanyEnrich API key to run lead research. Create one at
> https://app.companyenrich.com/access-keys and set it as `COMPANYENRICH_API_KEY`
> in your environment, then ask me again."

Do not ask the user to paste the key into the chat, and do not write it to memory, notes, or
any file. Never print the key.

Each run makes three API calls that spend credits from the user's CompanyEnrich account.

## API Calls

All endpoints use `Authorization: Bearer {API_KEY}` header.

### 1. Person Lookup

POST `https://api.companyenrich.com/people/lookup`
Body: `{"email": "the-email"}`

Response has an `experiences` array. Pick the best one:
- **First priority:** `isMatched: true` (this is the experience matching the email domain)
- **Fallback:** `isCurrent: true`

From the chosen experience, extract: `position`, `seniority`, `department`, `company.name`
From root level: `name`, `first_name`, `last_name`, `location.address`, `socials.linkedin_url`

### 2. Company Enrichment

GET `https://api.companyenrich.com/companies/enrich?domain={domain}`

Extract:
- `name`, `description`, `categories` (array)
- `financial.total_funding` (number, format as $XM or $XK)
- `financial.funding_stage` (e.g. "series_a" becomes "Series A")
- `financial.funding[]` each with: `date` (first 10 chars), `amount` (format nicely),
  `type` (strip " - CompanyName" suffix), `from` (investor)

### 3. Workforce

GET `https://api.companyenrich.com/companies/workforce?domain={domain}`

Extract:
- `department_headcount` (object: dept_name -> count)
- `observed_employee_count`, `employee_count_range`
- `history[]` for trends: compare `history[0]` vs `history[1]`, flag departments with >15% change

Format department names: replace underscores with spaces, title case.

## Display

Present results as a clean, readable report directly in chat. Include:

**Person:** name, position, seniority, department, location, LinkedIn link
**Company:** name, categories, full description
**Funding:** total raised, stage, each round (type, amount, investor, date)
**Workforce:** department headcount table, total employees, range
**Trends:** departments with significant changes (>15%), showing direction and percentage
