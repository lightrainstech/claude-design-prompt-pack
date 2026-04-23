---
name: repo-bootstrap
description: Create the GitHub-ready folder structure, README, manifest, and base repo files. Triggers: "set up the repo", "create the folder pack", "bootstrap the repository", "initialize skill repo", "start a new prompt pack".
---

# Repo Bootstrap

Creates a complete, publishable skill repository from scratch. This is the foundation skill — everything else runs after this.

## When to Use

**Trigger phrases (exact match):**
- "set up the repo"
- "create the folder pack"
- "bootstrap the repository"
- "initialize skill repo"
- "start a new prompt pack"
- "build the structure"
- "make the skeleton"

**Not a trigger if:**
- The user asks to edit existing files (that's editing, not bootstrapping)
- The folder structure already exists and is valid
- The user explicitly says "don't create anything, just tell me what to do"

---

## Before Starting

Ask (or infer) these if not obvious:

1. **Repo name:** What is this pack called? (Used in folder name, README title, manifest)
2. **Purpose:** 1-sentence summary of what this pack does
3. **Primary audience:** Who will use this? (developers, designers, marketers, etc.)
4. **Skills to include:** How many skills are planned? (affects folder structure)
5. **Brand file:** Does a brand file already exist? If not, flag that `brand-system-builder` needs to run.

**Default if not specified:**
- Repo name: derived from purpose or "prompt-pack-{timestamp}"
- Skills count: 1 (single-skill repo)
- Brand file: create placeholder to be filled

---

## Output Structure

### Required Folder Tree

```
{repo-name}/
├── README.md                    # Repo overview, installation, usage
├── MANIFEST.md                  # Machine-readable index of all files
├── CLAUDE.md                    # Repo rules for Claude/AI agents
├── skills/                      # All skill definitions
│   ├── {skill-1}/
│   │   └── SKILL.md             # Primary skill file
│   ├── {skill-2}/
│   │   └── SKILL.md
│   └── {skill-N}/
│       └── SKILL.md
├── references/                  # Shared reference files (optional)
│   ├── {reference-file}.md
│   └── ...
├── scripts/                     # Helper scripts (optional)
│   └── {script}.py
└── assets/                      # Images, templates (optional)
    └── ...
```

### Optional Folders (add only if needed)

| Folder | When to add |
|--------|-------------|
| `references/` | Multiple skills share documentation or checklists |
| `scripts/` | Automation needed (linting, packaging, generation) |
| `assets/` | Images, fonts, or binary files included in the pack |
| `templates/` | Reusable templates used across skills |

---

## Step-by-Step Process

### Step 1: Validate the Working Directory

Check what exists:

```
ls -la
```

**Three scenarios:**

| Scenario | Condition | Action |
|----------|-----------|--------|
| A. Empty dir | Only .git/ or nothing | Start fresh |
| B. Partial structure | Some files exist but incomplete | Audit what exists, fill gaps |
| C. Complete | All required files present | Verify validity, report "already done" |

**Scenario A — Start fresh:**
```bash
mkdir -p skills/{skill-name} references scripts assets
touch README.md MANIFEST.md CLAUDE.md
```

**Scenario B — Audit first:**
```bash
ls -la skills/ 2>/dev/null || echo "No skills folder"
ls -la references/ 2>/dev/null || echo "No references folder"
cat README.md 2>/dev/null || echo "No README"
```

Then fill gaps based on what's missing.

**Scenario C — Verify:**
```bash
# Check README has required sections
# Check MANIFEST.md parses as valid list
# Check CLAUDE.md has repo rules
```

If valid, tell the user: "Repo structure is complete. Run 'skills health-check' to verify contents."

---

### Step 2: Create README.md

**Required sections (in order):**

```markdown
# {Repo Name}

{One-line description of what this pack does}

## What This Pack Contains

{Bullet list of skills/features included}

## Quick Start

{3-step installation/usage guide:
1. Clone/download
2. Copy to your prompt library
3. First usage example
}

## Skills

| Skill | Purpose | Trigger |
|-------|---------|---------|
| {skill-name} | {one-line purpose} | {trigger phrase} |
| ... | ... | ... |

## Requirements

{Any tools, software, or context needed to use this pack}

## Examples

```
{One concrete example of usage}
```

## Contributing

{How to extend or modify this pack}

---
{Optional: license, author, date}
```

**Rules for README:**
- No corporate language ("world-class", "cutting-edge")
- No filler ("In today's fast-paced world...")
- Lead with what it does, not why it matters
- Include one working example

---

### Step 3: Create MANIFEST.md

**Format:** One file per line, with metadata

```markdown
---
version: 1.0.0
generated: {YYYY-MM-DD}
repo: {repo-name}
---

# Files

## Core
README.md                    | text/markdown | required | overview
MANIFEST.md                  | text/markdown | required | index
CLAUDE.md                    | text/markdown | required | agent rules

## Skills
skills/{skill-name}/SKILL.md | text/markdown | required | primary skill

## References
references/{ref-name}.md     | text/markdown | optional | shared docs

## Scripts
scripts/{script-name}.py     | text/python   | optional | automation

## Assets
assets/{asset-name}.{ext}    | binary        | optional | images/media
```

**Rules for MANIFEST:**
- One entry per file
- Include type (text/binary)
- Mark required vs. optional
- Brief description in last column
- Keep sorted by category

---

### Step 4: Create CLAUDE.md

**Template:**

```markdown
# CLAUDE.md — Agent Rules for This Repo

## Purpose
{One paragraph explaining what this repo contains and when to use it}

## Repo Structure
{File tree overview}

## Skill Locations
- Skills: `skills/{skill-name}/SKILL.md`
- References: `references/`
- Scripts: `scripts/`

## Key Conventions
- Follow existing naming patterns
- Keep outputs modular
- Verify before committing

## When to Trigger Skills
| Situation | Trigger |
|-----------|---------|
| {situation 1} | {skill-name} |
| {situation 2} | {another-skill} |

## Current Status
{What exists vs. what's planned}

## Known Issues
{Any limitations or todos}
```

---

### Step 5: Create First Skill File (Placeholder)

If no skills exist yet, create a placeholder:

```markdown
---
name: {skill-name}
description: "One-line purpose statement"
---

# {Skill Name}

## When to Use

**Trigger phrases:** "..."

## What This Does

{2-3 sentences on purpose}

## Coming Soon

{Placeholder — fill in before publishing}
```

This ensures the folder structure is valid even if skills aren't written yet.

---

### Step 6: Final Validation

Run this checklist:

| Check | Command | Pass if |
|-------|---------|---------|
| README exists | `test -f README.md && echo "OK"` | "OK" |
| MANIFEST exists | `test -f MANIFEST.md && echo "OK"` | "OK" |
| CLAUDE.md exists | `test -f CLAUDE.md && echo "OK"` | "OK" |
| Skills folder exists | `test -d skills && echo "OK"` | "OK" |
| Folders named correctly | `ls skills/` | Lowercase, hyphenated |
| No forbidden files | `ls *.md` | Only allowed .md files at root |

**Forbidden at root level:**
- `NOTES.md`
- `TODO.md`
- `CHANGELOG.md` (unless intentional)
- Any file with uppercase in name

---

## Output for User

After bootstrapping, report:

```
✓ Repo created: {repo-name}
✓ Folder structure: {tree output}
✓ Next steps:
  1. Add your first skill → skills/{skill-name}/SKILL.md
  2. Run brand-system-builder if no brand file exists
  3. Test with: opencode → "help" → load skill
```

---

## Cross-Skill Orchestration

**Calls after bootstrapping:**

| Skill | When to call | What to pass |
|-------|--------------|--------------|
| `brand-system-builder` | If no brand file exists | Repo name, audience |
| `prompt-author` | If skills need prompts written | Skill specs |
| `packaging-and-export` | When repo is complete and ready to publish | Final folder path |

**Depends on:**
- None (this is the foundation skill)

---

## Edge Cases

| Situation | Handling |
|-----------|----------|
| User provides partial structure | Fill gaps, preserve existing files |
| User provides conflicting structure | Ask: "Keep existing or replace?" |
| Name has spaces | Convert to kebab-case automatically |
| Name has uppercase | Convert to lowercase automatically |
| User wants custom folders | Ask for rationale, add if justified |
| Skills folder empty | Create placeholder skill file |

---

## Done Checklist

Before declaring complete:

- [ ] README.md has all required sections
- [ ] MANIFEST.md is valid format and lists all files
- [ ] CLAUDE.md has repo rules and skill triggers
- [ ] skills/ folder exists with at least one skill file
- [ ] No forbidden files at root
- [ ] All folder names are lowercase, hyphenated
- [ ] User sees clear "next steps" summary