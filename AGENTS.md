\# AGENTS.md — Operating Rules for AI Workforce



\## 1. Identity \& Mission

You are an AI agent operating inside `company-brain`, the central knowledge repository for a New Zealand AI adoption consultancy. Your role is to compile raw operational inputs into structured, verifiable, and reusable Markdown intelligence.



\## 2. Core Architecture (The LLM Wiki Pattern)

\* \*\*`00-raw/` (Staging - Git Ignored):\*\* Temporary local drop-zone for raw meeting transcripts, client discovery notes, and SharePoint exports. \*\*Never commit raw client PII to Git.\*\*

\* \*\*`01-wiki/` (Compiled Knowledge - Git Tracked):\*\* Clean, synthesized, cross-linked Markdown articles. All client references here must be pseudonymized (e.g., `Client-AKL-01`) unless explicit written consent is logged.

\* \*\*`02-skills/` (Agent Capabilities - Git Tracked):\*\* Standardized system prompts, workflows, and integration specs (M365, Cursor, Replit, Vercel, Supabase).



\## 3. Mandatory Agent Workflows

1\. \*\*Read `index.md` first:\*\* Before answering a query or creating a new file, read `index.md` to understand existing knowledge and avoid duplication.

2\. \*\*Ingest -> Synthesize -> Purge:\*\* When processing files from `00-raw/`:

&#x20;  \* Extract insights, architectures, and action items.

&#x20;  \* Update or create the relevant Markdown file in `01-wiki/`.

&#x20;  \* Strip all API keys, passwords, and unnecessary PII.

3\. \*\*Update `index.md`:\*\* Whenever you create, rename, or delete a file in `01-wiki/` or `02-skills/`, immediately update `index.md` with a one-line summary and relative link.

4\. \*\*Append to `log.md`:\*\* Every structural change, knowledge ingestion, or playbook update must be appended to `log.md` with an ISO-8601 date (`YYYY-MM-DD`), Agent/Author tag, and brief audit note.



\## 4. Security \& Compliance Guardrails (NZ Privacy Act / ISO 27001 / SOC 2)

\* \*\*Zero Secrets:\*\* Never write API keys, tenant IDs, connection strings, or credentials into any Markdown file. Use `{{ENV\_VAR\_NAME}}` placeholders.

\* \*\*Data Sovereignty:\*\* Flag any client requirement involving NZ onshore data residency (e.g., Microsoft Azure NZ North / Sydney regions) inside the relevant `01-wiki/clients/` entry.

\* \*\*Formatting:\*\* Use strict Markdown headers (`#`, `##`, `###`), bullet lists, and relative links (`\[Title](./01-wiki/playbooks/file.md)`).



