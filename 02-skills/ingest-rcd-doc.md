# Skill: Ingest & Synthesize `RCD Internal` Documentation 
 
> **Skill ID:** SKILL-001 | **Target Folder:** `00-raw/` → `01-wiki/`   
> **Compliance Rule:** Strip all PII, client names, financial bank details, and secrets before writing to `01-wiki/`. 
 
## 1. Trigger 
Run this skill whenever raw files from the M365 SharePoint **`RCD Internal`** library are staged in `00-raw/`. 
 
## 2. Execution Steps (Mandatory Sequence) 
1. **Read Governance:** Read `AGENTS.md` and `index.md` first to understand existing folder taxonomy and avoid duplicate articles. 
2. **Audit `00-raw/`:** List all files currently inside `00-raw/` and classify each by destination: 
   * Service offerings, pricing models, delivery frameworks → `01-wiki/playbooks/` 
   * Tech stack specs, M365/Supabase/Vercel setups → `01-wiki/architecture/` 
   * Client discovery notes, proposals, case studies → `01-wiki/clients/` (must pseudonymize as `Client-NZ-01`, `Client-WKO-01`, etc.) 
   * Policies, privacy statements, security controls → `01-wiki/nz-compliance/` 
3. **Sanitize & Synthesize:** 
   * Extract core facts, frameworks, decisions, and reusable templates. 
   * Strip all personal names, email addresses, phone numbers, IRD/NZBN numbers (unless public company metadata), and API credentials. 
   * Format output into clean, scannable Markdown with clear `#` headings, bullet points, and tables. 
4. **Update Master Index:** Add a relative link and one-line summary for every new or updated article inside `index.md`. 
5. **Append Audit Log:** Add a timestamped entry to `log.md` (`YYYY-MM-DD | [AGENT] | Ingested <filename> into <target-path>`). 
6. **Confirm Purge Readiness:** Output a checklist of processed files in `00-raw/` so the human founder can safely delete them before committing to Git.