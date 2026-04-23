---
name: packaging-and-export
description: Prepare and package GitHub-ready ZIP bundles and downloadable repository artifacts. Triggers: "package it", "zip the repo", "make it downloadable", "export the pack", "prepare for download", "bundle it".
---

# Packaging And Export

Packages a completed skill repository into a distribution-ready format — clean ZIP bundles, validated manifests, and publishable artifacts.

## When to Use

**Trigger phrases (exact match):**
- "package it"
- "zip the repo"
- "make it downloadable"
- "export the pack"
- "prepare for download"
- "bundle it"
- "create release"
- "package for distribution"

**Also triggers if:**
- User says "it's ready, publish it"
- `repo-bootstrap` is complete and user wants to distribute
- User asks "what files would I share?"

**Not a trigger if:**
- User asks to edit content (that's editing, not packaging)
- Repo is incomplete (package only complete repos)
- User asks for GitHub release specifically (that's GitHub workflow)

---

## Before Starting

Ask (or infer) these:

1. **Source path:** Where is the repo to package? (default: current directory)
2. **Package name:** What should the ZIP be called? (default: repo name)
3. **Version:** Is this a specific version or latest? (affects filename)
4. **Destination:** Where to save the package? (default: same parent directory as repo)
5. **Include files:** Any specific files to include/exclude?
6. **Git history:** Include `.git` folder? (default: NO — clean package)

**Default if not specified:**
- Source: current working directory
- Package name: derived from repo folder name
- Version: `latest`
- Destination: parent of source directory
- Git history: excluded

---

## Step-by-Step Process

### Step 1: Validate the Source Repository

Before packaging, verify the repo is package-ready:

**Required files check:**
```bash
test -f README.md && echo "README: OK"
test -f MANIFEST.md && echo "MANIFEST: OK"
test -f CLAUDE.md && echo "CLAUDE: OK"
test -d skills && echo "SKILLS: OK"
```

**Manifest validation:**
- Does MANIFEST.md list all files?
- Are all listed files present?
- Are paths correct (no broken links)?

**If validation fails:**
```
STOP. Fix these issues before packaging:
1. Missing {file}
2. MANIFEST.md out of sync with actual files
3. skills/ folder empty or missing
```

---

### Step 2: Determine Include/Exclude Rules

**Always EXCLUDE:**
```
.git/                    # Git history
.DS_Store               # macOS artifacts
Thumbs.db               # Windows artifacts
node_modules/           # Dependencies
.env                    # Environment files
*.log                   # Log files
dist/                   # Build outputs (if applicable)
```

**Always INCLUDE:**
```
README.md               # Essential
MANIFEST.md             # Essential
CLAUDE.md               # Essential for AI tools
skills/                 # Skill definitions
```

**Conditional (include if present):**
```
brand.md               # If exists
references/            # If exists and non-empty
scripts/               # If exists and non-empty
assets/                # If exists and non-empty
```

---

### Step 3: Create Exclusion Script

```bash
# Create .packignore file (like .gitignore but for packaging)
cat > .packignore << 'EOF'
.git
.DS_Store
Thumbs.db
node_modules
.env
*.log
dist
EOF
```

**Alternative: Use rsync with exclusions**
```bash
rsync -av --exclude='.git' \
         --exclude='.DS_Store' \
         --exclude='node_modules' \
         --exclude='*.log' \
         --exclude='.env' \
         ./source-folder/ ./package-folder/
```

---

### Step 4: Build the Package

**Standard ZIP package:**

```bash
# Navigate to parent directory
cd /path/to/parent

# Create package name with version if specified
PACKAGE_NAME="prompt-pack-name"
VERSION="v1.0.0"
OUTPUT="${PACKAGE_NAME}-${VERSION}.zip"

# Package (exclude .git and other artifacts)
zip -r "${OUTPUT}" "./${PACKAGE_NAME}" \
    -x "*.git*" \
    -x "*.DS_Store" \
    -x "*.log" \
    -x "node_modules/*" \
    -x ".env"
```

**Verify the package contents:**
```bash
unzip -l "${OUTPUT}" | head -30
```

**Expected output:**
- README.md at root
- MANIFEST.md at root
- CLAUDE.md at root
- skills/ folder with all skills
- No .git folder
- No node_modules

---

### Step 5: Generate Package Manifest (Human-Readable)

Create `PACKAGE.md` inside the ZIP or alongside it:

```markdown
# {Package Name} — {Version}

**Created:** {YYYY-MM-DD HH:MM}
**Files:** {count}
**Size:** {size in KB/MB}

## What's Included

### Core Files
| File | Purpose |
|------|---------|
| README.md | Installation and usage guide |
| MANIFEST.md | Machine-readable file index |
| CLAUDE.md | Agent rules for this repo |

### Skills
| Skill | Trigger Phrases |
|--------|-----------------|
| {skill-name} | "{phrase}", "{phrase}" |

### Optional Components
| Folder | Contents |
|--------|----------|
| references/ | Shared documentation |
| scripts/ | Helper scripts |
| assets/ | Images and templates |

## Installation

1. Download `{package-name}-{version}.zip`
2. Extract to your prompts folder
3. Load skill: `{how to load}`
4. Run: `{first command}

## Requirements

{Any dependencies or prerequisites}

## Changelog

### {Version}
- {Change 1}
- {Change 2}

---

*Generated by packaging-and-export skill*
```

---

### Step 6: Create Checksum

Generate checksums for verification:

```bash
# MD5 (fast, for basic verification)
md5sum "{package-name}.zip"

# SHA256 (secure, for releases)
sha256sum "{package-name}.zip"
```

**Output format:**
```
{password_hash}  {package-name}.zip
```

**Store checksums in:**
- `CHECKSUMS.txt` alongside ZIP
- Or in RELEASE_NOTES.md

---

### Step 7: Post-Package Validation

Run this checklist:

| Check | Command | Pass if |
|-------|---------|---------|
| ZIP exists | `test -f {name}.zip` | "OK" |
| ZIP not empty | `unzip -l {name}.zip | wc -l` | > 10 lines |
| No .git folder | `unzip -l {name}.zip | grep .git` | (empty) |
| README.md present | `unzip -l {name}.zip | grep README` | (found) |
| MANIFEST.md present | `unzip -l {name}.zip | grep MANIFEST` | (found) |
| No forbidden files | `unzip -l {name}.zip | grep -E '(node_modules|\.log|\.env)'` | (empty) |

---

## Output Format

### Primary Output: ZIP File

**Filename pattern:**
```
{package-name}-{version}.zip
```

**Examples:**
- `lightrains-prompts-latest.zip`
- `bento-layout-pack-v1.0.0.zip`
- `prompt-author-suite-v0.5.0.zip`

---

### Secondary Output: Companion Files

| File | When to create |
|------|----------------|
| `CHECKSUMS.txt` | Always (for verification) |
| `PACKAGE.md` | Always (human guide) |
| `RELEASE_NOTES.md` | If versioned release |
| `INSTALL.sh` | If installation is complex |

---

### Manifest Updates

After packaging, update `MANIFEST.md` to add:

```markdown
## Package Distribution

| Artifact | File | Checksum (SHA256) |
|----------|------|-------------------|
| Latest ZIP | {name}-latest.zip | {hash} |
| Version {ver} | {name}-{ver}.zip | {hash} |

**Last packaged:** {YYYY-MM-DD}
**Packaged by:** packaging-and-export skill
```

---

## Packaging Modes

### Mode 1: Latest (Default)

Packages the current state as `*-latest.zip`.

**Use when:**
- Sharing work-in-progress for feedback
- Internal distribution
- Frequent updates

**Filename:** `{name}-latest.zip`

---

### Mode 2: Versioned Release

Packages with explicit version.

**Use when:**
- Official release
- User wants specific version
- Changelog is maintained

**Filename:** `{name}-{semver}.zip`

**Version format:**
- Major.Minor.Patch: `1.0.0`
- Pre-release: `1.0.0-beta.1`
- Date-based fallback: `v2026.04.23`

---

### Mode 3: Selective (Subset)

Packages only specific folders or files.

**Use when:**
- User wants only one skill from a multi-skill repo
- Partial release of new content

**Command:**
```bash
zip -r output.zip skills/skill-name/
# or
zip -r output.zip references/ prompts/
```

---

### Mode 4: Preview (With Metadata)

Packages content plus generated metadata.

**Use when:**
- User wants to review before publishing
- QA testing

**Includes:**
- All standard content
- `INTERNAL_NOTES.md` (for reviewer eyes only)
- `TODO.md` (what's left to do)

---

## Common Issues and Fixes

### Issue 1: Package Too Large

**Symptoms:** ZIP > 50MB

**Causes:**
- Large asset files
- Included node_modules
- Backup files

**Fix:**
```bash
# Find large files
find . -type f -size +1M

# Compress images
find ./assets -name "*.png" -exec convert {} -quality 80 {} \;

# Remove duplicates
find . -type d -name "*copy*" -exec rm -rf {} \;
```

---

### Issue 2: Broken Symlinks

**Symptoms:** "symlink has no target" warnings

**Fix:**
```bash
# Replace symlinks with copies for packaging
find . -type l -exec sh -c '
  target=$(readlink "$1")
  rm "$1"
  cp -r "$target" "$1"
' _ {} \;
```

---

### Issue 3: MANIFEST Out of Sync

**Symptoms:** MANIFEST.md lists files that don't exist

**Fix:**
```bash
# Regenerate MANIFEST from actual files
find . -type f ! -path './.git/*' ! -name '.DS_Store' \
    | sort | while read f; do
    echo "$f | text/markdown | found | generated"
done > MANIFEST.md
```

---

### Issue 4: Accidentally Included Secrets

**Symptoms:** ZIP contains `.env`, API keys, credentials

**Prevention:**
- Always check for `.env` and `*.key`
- Use pre-package scan:

```bash
# Scan for potential secrets
rg -l "API_KEY|SECRET|PASSWORD|TOKEN" . || echo "No secrets found"
```

**If found:**
```bash
# Remove from package
zip -d output.zip ".env" "config/secrets.yml"
```

---

## Done Checklist

Before declaring complete:

- [ ] Source repo validated (all required files present)
- [ ] MANIFEST.md is in sync with actual files
- [ ] Unwanted files excluded (.git, node_modules, logs, .env)
- [ ] ZIP created with correct name
- [ ] Package contents verified with `unzip -l`
- [ ] CHECKSUMS.txt generated (MD5 and SHA256)
- [ ] PACKAGE.md created with install instructions
- [ ] No secrets or credentials in package
- [ ] User receives:
  - ZIP file path
  - Checksums
  - Instructions for installing
  - Link to documentation (README)

---

## Cross-Skill Orchestration

**Called by:**
- User directly (when ready to share/distribute)
- `repo-bootstrap` — when repo is complete (optional prompt)

**Feeds into:**
- GitHub upload (if user wants to publish)
- Download server (if hosting downloads)
- Distribution manifest (if tracking multiple packages)

**Depends on:**
- `repo-bootstrap` — source must have valid structure
- All skills should be complete before packaging (not required, but recommended)

---

## Edge Cases

| Situation | Handling |
|-----------|----------|
| Source repo is empty | Refuse to package. "Nothing to package — repo is empty." |
| No MANIFEST.md | Generate one before packaging. "Missing MANIFEST.md — generating..." |
| Package name has spaces | Convert to hyphens: "My Pack" → "my-pack" |
| User wants multiple versions | Create subfolders: `releases/v1.0.0/`, `releases/v2.0.0/` |
| Very large assets | Suggest optimization or external hosting (link, don't include) |
| Package for different platforms | Create platform-specific variants: `*-mac.zip`, `*-linux.zip` |
| Git history needed | Ask user explicitly: "Include .git folder? (usually no)" |
| Package is for internal use | Skip external hosting instructions, focus on local install |