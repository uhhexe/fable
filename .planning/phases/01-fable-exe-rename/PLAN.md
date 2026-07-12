# fable.exe v2 Rename Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use `executing-plans` to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish a complete, verified breaking rename from fable v1 to fable.exe v2 without leaving mixed install paths or active public URLs.

**Architecture:** Keep `fable.exe` as the public brand and use `fable-exe` for Claude Code identifiers that must remain kebab-case. Preserve v1 evaluation artifacts as historical evidence while migrating every active distribution surface atomically.

**Tech Stack:** Claude Code plugin manifests and skills, static HTML/CSS/JavaScript, GitHub Pages, GitHub Releases.

---

### Task 1: Record the migration contract

**Files:**
- Create: `docs/superpowers/specs/2026-07-12-fable-exe-rename-design.md`
- Create: `.planning/phases/01-fable-exe-rename/PLAN.md`

- [x] **Step 1: Lock the brand/identifier split and historical-evidence rule**
- [x] **Step 2: Commit the plan and design record**

Run: `git diff --check`
Expected: no output.

### Task 2: Rename the plugin and skills

**Files:**
- Modify: `.claude-plugin/plugin.json`
- Modify: `.claude-plugin/marketplace.json`
- Rename and modify: `skills/fable-*/SKILL.md` to `skills/fable-exe-*/SKILL.md`

- [x] **Step 1: Rename the six skill directories and frontmatter identifiers**
- [x] **Step 2: Update active trigger phrases and sibling references**
- [x] **Step 3: Set plugin and marketplace version/name metadata to `fable-exe` 2.0.0**
- [x] **Step 4: Validate JSON and the plugin**

Run: `python3 -m json.tool .claude-plugin/plugin.json >/dev/null && python3 -m json.tool .claude-plugin/marketplace.json >/dev/null && claude plugin validate .`
Expected: both JSON files parse and Claude reports validation success without warnings.

### Task 3: Migrate public documentation and the site

**Files:**
- Modify: `README.md`
- Modify: `docs/SPEC.md`
- Modify: `docs/index.html`
- Modify: `docs/og-card.png`
- Modify: `evals/README.md`

- [ ] **Step 1: Replace active branding, URLs, commands, and skill IDs**
- [ ] **Step 2: Add explicit v1-to-v2 migration instructions**
- [ ] **Step 3: Label the unchanged v1 evaluation artifacts as historical**
- [ ] **Step 4: Regenerate the Molten social card for fable.exe v2.0.0**
- [ ] **Step 5: Verify active-copy stale-token allowlist**

Run: `rg -n 'uhhexe/fable($|[^.])|github.io/fable/|fable@fable|skills/fable-(mode|plan|spec|review|grill|delegate)' README.md docs .claude-plugin skills`
Expected: only intentional migration/history references remain.

### Task 4: Verify the local release candidate

**Files:**
- Test: repository root and `docs/index.html`

- [ ] **Step 1: Run plugin validation and a disposable local install**
- [ ] **Step 2: Confirm all six `fable-exe-*` skills are installed**
- [ ] **Step 3: Browser-check desktop, mobile, copy command, console, and overflow**
- [ ] **Step 4: Commit the verified release candidate**

Run: `claude plugin validate .`
Expected: validation succeeds with no warnings.

### Task 5: Publish and prove v2.0.0

**Surfaces:**
- GitHub PR, repository settings, Pages, release, local installed plugin

- [ ] **Step 1: Open one PR and confirm it is mergeable**
- [ ] **Step 2: Merge the PR and rename the repository to `fable.exe`**
- [ ] **Step 3: Update description/homepage and publish release `v2.0.0`**
- [ ] **Step 4: Verify the new Pages page and social card**
- [ ] **Step 5: Clean-install `fable-exe@fable-exe` from `uhhexe/fable.exe` and migrate the live local installation**
- [ ] **Step 6: Confirm main, tag, release, and installed skill inventory**

Run: `gh release view v2.0.0 --repo uhhexe/fable.exe --json tagName,targetCommitish,url`
Expected: a published v2.0.0 release targeting the renamed repository.
