# Claude Prompt Pack Skill Repo

A production-ready skill repository for creating, packaging, and distributing Claude/AI design workflows, bento-grid visuals, and reusable prompt systems.

Maintained by [Lightrains Technolabs](https://lightrains.com?ref=ccskill01).

---

## What This Repo Does

This repo provides a structured workflow to:

1. Bootstrap a new skill repository from scratch
2. Define brand voice and visual rules
3. Author high-quality AI prompts
4. Design bento-grid visual layouts
5. Package everything for distribution

---

## Use Cases

### For Internal Teams

- **Standardize workflows** — Every team member uses the same prompts → consistent output
- **Shared brand rules** — One source of truth for voice, colors, and style
- **Faster onboarding** — New team members read the brand file, not guess

### For Agencies

- **Client-ready deliverables** — Bootstrap a repo per client with their brand rules
- **Professional packaging** — Clean ZIP with checksums and install guide
- **Consistent output** — Same quality bar across all projects

### For Solo Builders

- **Don't rewrite from scratch** — Reusable prompts and layouts
- **Fast turnaround** — Structured workflow means less decision overhead
- **Professional results** — Brand system and quality checklists built in

### For Prompt Library Builders

- **Organize by type** — Image, text, workflow prompts in one place
- **Easy export** — Package subsets or full library for sharing
- **Extendable** — Add skills as your library grows

### Team Collaboration Features

| Feature | How it helps |
|---------|--------------|
| Shared brand file | Everyone references the same rules |
| Trigger phrases | Natural language works for all team members |
| Quality checklists | Each skill has a "done" list for review |
| Manifest system | Always know what's in the repo |
| CLAUDE.md | AI agent follows same rules as humans |

---

## Repository Structure

```
├── CLAUDE.md                    # Agent rules for Claude/opencode
├── README.md                    # This file
├── MANIFEST.md                  # Machine-readable file index
├── skills/                      # All skill definitions
│   ├── repo-bootstrap/          # Foundation: create repo structure
│   ├── brand-system-builder/     # Brand voice and visual rules
│   ├── prompt-author/           # Write reusable prompts
│   ├── bento-layout-director/  # Design bento-grid layouts
│   └── packaging-and-export/    # ZIP and publish
└── (add as needed)
    ├── references/              # Shared docs
    ├── scripts/                 # Automation
    └── assets/                  # Images/templates
```

---

## Skills Overview

| Skill                     | Purpose                           | Trigger Phrases                                                         |
| ------------------------- | --------------------------------- | ----------------------------------------------------------------------- |
| **repo-bootstrap**        | Create the complete repo skeleton | "set up the repo", "bootstrap the repository", "create the folder pack" |
| **brand-system-builder**  | Define voice, colors, typography  | "build the brand file", "define brand voice", "brand guidelines"        |
| **prompt-author**         | Write reusable prompts for AI     | "write the master prompt", "create a prompt", "compose a prompt"        |
| **bento-layout-director** | Design modular card layouts       | "make it bento", "arrange in tiles", "design grid layout"               |
| **packaging-and-export**  | ZIP and prepare for download      | "package it", "zip the repo", "export the pack"                         |

---

## Usage

### Quick Start

```bash
# 1. Bootstrap a new repo
"set up the repo for my-prompt-pack"

# 2. Define brand rules
"build the brand file for a premium SaaS brand"

# 3. Write prompts
"write the master prompt for a dashboard image"

# 4. Design the layout
"make it bento with 4 feature tiles"

# 5. Package for distribution
"package it and give me a ZIP"
```

### Skill Chaining

Use skills in this order for complete projects:

```
repo-bootstrap → brand-system-builder → prompt-author → bento-layout-director → packaging-and-export
```

Not every project needs all 5. Use what fits.

### Single Skill Use

If the task is simple, use one skill only:

| Task                                 | Skill                   |
| ------------------------------------ | ----------------------- |
| Start a new repo from scratch        | `repo-bootstrap`        |
| Define how content should sound/look | `brand-system-builder`  |
| Write a specific prompt              | `prompt-author`         |
| Plan a visual grid                   | `bento-layout-director` |
| Prepare files for sharing            | `packaging-and-export`  |

---

## Each Skill in Detail

### 1. repo-bootstrap

**What it creates:**

- `README.md` with installation and usage
- `MANIFEST.md` with file index
- `CLAUDE.md` with agent rules
- Empty `skills/` folder with first placeholder skill

**What it asks for:**

- Repo name
- Purpose (1 sentence)
- Number of skills planned

**Output:** Ready-to-publish repo structure

---

### 2. brand-system-builder

**What it creates:**

- `BRAND.md` with voice dimensions, vocabulary, color palette
- 5-point scale for: Formality, Optimism, Playfulness, Competence, Novelty
- Use/ban vocabulary lists
- 3 content examples (good)
- 2 anti-examples (bad + fix)
- Channel adaptations table

**What it asks for:**

- Brand name
- Industry/domain
- 3 examples of existing content (or "make something up")

**Output:** Complete brand rules file

---

### 3. prompt-author

**What it creates:**

- Single prompts or prompt collections
- Templates with variables
- Platform-specific syntax (Claude, Midjourney, DALL-E, etc.)

**Prompt types supported:**

- **Image prompts** — subject, style, composition, mood
- **Text prompts** — role, context, task, constraints, format, tone
- **Workflow prompts** — chained multi-step processes

**What it asks for:**

- Deliverable type (image/text/workflow)
- Subject and audience
- Target platform

**Output:** Production-ready prompts with usage examples

---

### 4. bento-layout-director

**What it creates:**

- ASCII layout diagrams
- Tile specifications (size, position, content)
- Spacing rules (4/8/16/24/32/48/64px scale)
- Color usage guidelines
- Platform adaptation notes (web/mobile)

**Layout patterns:**

- Equal grid (all tiles same size)
- Hero + supporting (one dominant)
- Asymmetric row (varied widths)
- Brick/mosaic (many small items)

**What it asks for:**

- Content items to arrange
- Hierarchy (equal or focal point?)
- Platform (web/mobile/presentation)

**Output:** Complete layout spec with ASCII diagram

---

### 5. packaging-and-export

**What it creates:**

- Clean ZIP package (excludes .git, node_modules, logs, secrets)
- `CHECKSUMS.txt` with MD5 and SHA256
- `PACKAGE.md` with installation guide
- Updated `MANIFEST.md`

**Packaging modes:**

- **Latest** — current state as `*-latest.zip`
- **Versioned** — explicit version as `*-v1.0.0.zip`
- **Selective** — only specific folders
- **Preview** — with internal notes for QA

**What it asks for:**

- Source path (defaults to current directory)
- Package name
- Version (or "latest")

**Output:** Distribution-ready ZIP with checksums

---

## Example Workflow

### Scenario: Create a brand prompt pack for distribution

```
User: "set up the repo for lightrains-design-prompts"

Agent: [runs repo-bootstrap]
Output: Creates folder structure, README, MANIFEST, CLAUDE.md

User: "build the brand file for a premium AI design studio"

Agent: [runs brand-system-builder]
Output: Creates BRAND.md with voice rules, colors, examples

User: "write the master prompt for a hero dashboard image"

Agent: [runs prompt-author]
Output: Creates prompts/dashboard-hero.md with full prompt

User: "make it bento with the dashboard as hero"

Agent: [runs bento-layout-director]
Output: Creates layout spec with ASCII diagram

User: "package it for GitHub release v1.0.0"

Agent: [runs packaging-and-export]
Output: lightrains-design-prompts-v1.0.0.zip + CHECKSUMS.txt
```

---

## Best Practices

### Naming Conventions

- Skill names: kebab-case (`repo-bootstrap`, not `repoBootstrap`)
- File names: kebab-case with hyphens
- Folders: lowercase, hyphenated

### Trigger Phrases

Each skill includes exact trigger phrases. Use them as guidance — natural language variations work too.

### Modularity

One skill, one purpose. If a skill does too much, it should be split.

### Cross-Skill Coordination

- `repo-bootstrap` runs first (foundation)
- `brand-system-builder` runs second (inputs for everything else)
- `prompt-author` runs when prompts are needed
- `bento-layout-director` consumes prompt output
- `packaging-and-export` runs last (finalizes everything)

### Quality Check

Each skill has a "done checklist." Run through it before declaring complete.

---

## Requirements

- Claude/opencode or compatible AI agent
- Basic terminal (for packaging)
- Optional: markdown preview for reviewing output

---

## Contributing

To add a new skill:

1. Create `skills/{skill-name}/SKILL.md`
2. Follow the anatomy: trigger phrases, process steps, quality rubric
3. Add to this README in the skills overview
4. Update MANIFEST.md
5. Test with: "load skill {skill-name}"

---

## License

MIT License. Use freely for personal and commercial projects.

---

## Related

- [Lightrains](https://lightrains.com) — where this repo is maintained
- [opencode](https://opencode.ai) — AI coding agent that runs these skills
