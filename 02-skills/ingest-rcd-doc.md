# Skill: Ingest, Synthesize & Delta-Sync `RCD Internal` Documentation

> **Skill ID:** SKILL-001 | **Version:** 1.1 | **Target Folder:** `00-raw/` -> `01-wiki/`  
> **Compliance Rule:** Strip all PII, client names, financial bank details, and secrets before writing to `01-wiki/`.

## 1. Trigger
Run this skill whenever new or revised files from the M365 SharePoint **`RCD Internal`** library are staged in `00-raw/`.

## 2. Execution Steps (Mandatory Sequence)

### Step 1: Read Governance & Check Existing Taxonomy
1. Read `AGENTS.md` and `index.md` first to map all existing articles in `01-wiki/`.
2. List all files currently staged inside `00-raw/`.

### Step 2: Mode Detection — New Ingestion vs. Delta Update
Before writing any file, determine whether the staged source document represents **net-new knowledge** or an **update to an existing topic**:

* **Mode A — Net-New Knowledge (Create):**
  If no existing article in `index.md` covers the subject, classify and create a new Markdown file in the matching destination:
  * Service offerings, pricing models, delivery frameworks -> `01-wiki/playbooks/`
  * Tech stack specs, M365/Supabase/Vercel setups, business architecture -> `01-wiki/architecture/`
  * Client discovery notes, proposals, case studies -> `01-wiki/clients/` (must pseudonymize as `Client-NZ-01`, `Client-WKO-01`, etc.)
  * Policies, privacy statements, security controls -> `01-wiki/nz-compliance/`

* **Mode B — Document Update & Delta-Sync (Merge — No Duplicates):**
  If `index.md` already lists an article covering the same topic (e.g., an updated Business Architecture, revised pricing tier, or amended SOP):
  1. **Do NOT create a duplicate file** (never create `-v2.md`, `-new.md`, or `-updated.md` copies—Git tracks version history).
  2. Read the existing `01-wiki/` target file in full.
  3. Perform a **semantic delta merge**:
     * Integrate new facts, architectural changes, and revised figures directly into the existing sections.
     * Supersede or remove outdated statements that conflict with the updated source document.
     * Preserve existing valid cross-links (`[Title](./path.md)`) and add new cross-links if new dependencies were introduced.
     * Update the document's metadata header (`Last Updated` / `Version` tag if present).

### Step 3: Sanitize & Format
* Strip all personal names, email addresses, phone numbers, IRD/NZBN numbers (unless public company metadata), and API credentials (`{{ENV_VAR_NAME}}`).
* Format output into clean, scannable Markdown with clear `#` headings, bullet points, and comparison tables.

### Step 4: Synchronize `index.md` & `log.md`
1. **Update `index.md`:**
   * For **Mode A (New):** Add a relative link and one-line summary under the matching category.
   * For **Mode B (Delta Update):** Verify the existing relative link remains intact and refine the one-line summary if the document's scope changed.
2. **Append Audit Entry to `log.md`:**
   * For **Mode A:** `YYYY-MM-DD | [AGENT] | Ingested <source-filename> into <target-path>`
   * For **Mode B:** `YYYY-MM-DD | [AGENT] | Delta-merged updated <source-filename> into <target-path> (superseded prior revision)`

### Step 5: Confirm Purge Readiness
Output a clear checklist of processed files in `00-raw/` so the human founder can delete the temporary staging copies and review the Git diff in GitHub Desktop before pushing to `main`.
