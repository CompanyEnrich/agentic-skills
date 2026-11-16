# GTM Skills for Claude Code

A collection of ready-to-use [Claude Code Skills](https://docs.anthropic.com/en/docs/claude-code/skills) for go-to-market teams. Drop them into your workflow and start researching leads, enriching contacts, and gathering prospect intel — all from your terminal.

Powered by [CompanyEnrich](https://companyenrich.com) APIs.

## Skills

| Skill | Description |
|-------|-------------|
| [Lead Research Agent](lead-research-agent/) | Full-pipeline lead research by email — person lookup, company enrichment, workforce trends |

## Quick Start

1. Sign up at [companyenrich.com](https://companyenrich.com) and grab your API key
2. Set it in your environment: `export COMPANYENRICH_API_KEY=your-api-key`
3. Install the skills into your agent:

   ```bash
   npx skills add CompanyEnrich/agentic-skills
   ```

4. Ask your agent to research a lead, for example `Research john@acme.com`

The skills live in [`skills/`](skills/) in the open `SKILL.md` format, so they work in Claude Code, Codex, Cursor, and other agents that support it.

### Claude chat

Each skill folder also has a packaged `.skill` file for Claude. Install it with `/skill install <skill-file>.skill`. That version asks for your API key on first run and keeps it in Claude's memory.

## Requirements

- An agent that supports skills, such as [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
- A [CompanyEnrich](https://companyenrich.com) API key

## License

MIT
