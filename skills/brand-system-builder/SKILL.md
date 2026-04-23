---
name: brand-system-builder
description: Build a complete brand rules file for prompt workflows. Triggers: "build the brand file", "create brand.md", "set brand rules", "define brand voice", "brand guidelines".
---

# Brand System Builder

Creates a comprehensive brand rules file that informs all other skills. Every skill that produces content should reference this file.

## When to Use

**Trigger phrases (exact match):**
- "build the brand file"
- "create brand.md"
- "set brand rules"
- "define brand voice"
- "brand guidelines"
- "create brand system"
- "write brand rules"

**Also triggers if:**
- Starting a new pack without existing brand file
- `repo-bootstrap` reports no brand file exists

**Not a trigger if:**
- A brand file already exists and is valid
- User asks to edit specific content (not brand rules)
- User wants a style guide for web/print (this is for prompt workflows only)

---

## Before Starting

Ask (or infer) these:

1. **Brand name:** What is this brand called?
2. **Industry/Domain:** What space does this brand operate in? (affects vocabulary)
3. **Audience:** Who are they talking to? (engineers, executives, consumers, etc.)
4. **Tone direction:** Pick one primary and one secondary
   - Primary: formal / casual / technical / playful / authoritative / friendly
   - Secondary: anything that complements
5. **Existing brand materials:** Does brand exist already? Logos, existing copy, website?
6. **Output path:** Where to save the brand file? (default: `{repo}/BRAND.md`)

**Default if not specified:**
- Brand name: derived from repo name
- Industry: technology/software
- Audience: professionals
- Tone: technical + direct
- Output: `BRAND.md` in repo root

---

## Output Structure

Creates `BRAND.md` with these sections:

```
1. Brand Overview
2. Voice Dimensions
3. Vocabulary Rules
4. Typography (if applicable)
5. Color Palette (if applicable)
6. Content Examples
7. Anti-Examples
8. Channel Adaptations
```

---

## Step-by-Step Process

### Step 1: Gather Brand Intelligence

Ask the user for:

**Minimum required:**
- 3 links to content the brand has published (blog posts, website, ads)
- 1 example of content they loved and want to emulate
- 1 example of content that felt wrong for the brand
- One sentence: "This brand sounds like ___"

**Nice to have:**
- Competitor brands they admire
- Influencers/writers who nail the tone
- Anti-examples of tone they want to avoid

**If user provides nothing:**
Use the default "technical + direct" persona and flag it as provisional.

---

### Step 2: Define Voice Dimensions

Rate the brand on these 5 dimensions (1-5 scale):

| Dimension | 1 | 2 | 3 | 4 | 5 |
|-----------|---|---|---|---|---|
| **Formality** | Casual, conversational | | Professional | | Formal, corporate |
| **Optimism** | Pessimistic/realistic | | Neutral | | Highly optimistic |
| **Playfulness** | Serious, no humor | | Light-hearted | | Very playful |
| **Competence** | Beginner-friendly | | Intermediate | | Expert-only |
| **Novelty** | Conventional | | Balanced | | Highly innovative |

**Scoring rules:**
- Always pick a number, never "depends"
- If unsure, default to 3
- Mark scores as "provisional" if based on limited samples

**Translate scores into guidance:**

| Score | What it means |
|-------|---------------|
| 1-2 on Formality | Use contractions. Short sentences. "You" not "one." First person. |
| 4-5 on Formality | Full sentences. No contractions. "The user" not "you." |
| 1-2 on Playfulness | No jokes. No metaphors. Dry facts only. |
| 4-5 on Playfulness | One joke per section. Metaphors welcome. Self-deprecation okay. |
| 1-2 on Competence | Define jargon. Explain basics. No assume knowledge. |
| 4-5 on Competence | Skip the basics. Use jargon. Assume the audience knows. |

---

### Step 3: Define Vocabulary Rules

**Positive list (use these words):**
- List 10-15 words that capture the brand voice
- Examples: "precise", "fast", "reliable", "honest", "battle-tested"

**Negative list (ban these words):**
- List 15-20 overused corporate/AI phrases
- Examples: "cutting-edge", "seamless", "leverage", "robust", "holistic"
- See Appendix A for full ban list

**Phrase patterns:**
- What kind of sentences does this brand use?
- Short and punchy? Long and flowing? Mix?
- Active voice only? Or，偶尔被动？

---

### Step 4: Define Visual Rules (if applicable)

If the brand system includes visual elements:

**Color palette:**
```
Primary:     #XXXXXX  (brand name)
Secondary:   #XXXXXX  (brand name)
Accent:      #XXXXXX  (brand name)
Neutral:     #XXXXXX  (brand name)
Background:  #XXXXXX  (brand name)
Text:        #XXXXXX  (brand name)
```

**Typography:**
```
Headlines:   {Font Name} — Bold
Body:        {Font Name} — Regular
Mono/Code:   {Font Name} — Regular
```

**Spacing scale (8px grid):**
- XS: 4px
- SM: 8px
- MD: 16px
- LG: 24px
- XL: 32px
- XXL: 48px

---

### Step 5: Write Content Examples

Create 3 examples of brand voice in action:

**Example 1 — Short form (one line)**
A product tagline, feature description, or headline.

**Example 2 — Medium form (2-3 sentences)**
A feature explanation, value prop, or landing page blurb.

**Example 3 — Long form (one paragraph)**
A full paragraph that shows how the voice holds up under pressure.

**Rules for examples:**
- Write real content, not placeholders
- If brand exists, derive from existing content
- If new brand, write aspirational content matching the dimensions
- Label each: "Strong brand voice ✓" or "Needs work ✗"

---

### Step 6: Write Anti-Examples

Create 2-3 examples of content that violates the brand rules:

**Format:**
```
❌ WRONG: {bad example}
   Why it's wrong: {specific violation}
   Fix: {how to fix it}

✓ RIGHT: {corrected example}
```

**Rules for anti-examples:**
- Use real-sounding bad examples, not obvious placeholders
- Match the subject matter of the brand
- Make violations specific, not vague ("too corporate")

---

### Step 7: Define Channel Adaptations

How does the voice adapt across formats?

| Channel | Voice adaptation |
|---------|-------------------|
| Technical docs | More formal. Complete sentences. Defined terms. |
| Marketing copy | Punchy. Benefit-led. Light adjectives okay. |
| Social media | Short. Can be more playful. Emoji optional. |
| Debug logs/errors | Direct. State the problem. State the fix. |
| Internal comms | More casual. Assume shared context. |

---

## Output Format

Create `BRAND.md` with this structure:

```markdown
# {Brand Name} — Brand System

> One-line description of how this brand sounds.

**Provisional:** Mark as provisional if based on limited samples.

---

## Voice Dimensions

| Dimension | Score | What this means |
|-----------|-------|------------------|
| Formality | 3/5 | Professional but approachable |
| Optimism | 3/5 | Realistic, honest assessments |
| Playfulness | 2/5 | Serious, no humor in content |
| Competence | 4/5 | Assumes audience knows the domain |
| Novelty | 3/5 | Balanced between familiar and fresh |

---

## Vocabulary

### Use These Words
- word 1
- word 2
- word 3

### Never Use These
- overused phrase 1
- overused phrase 2

---

## Voice in Action

### Example 1 — Short

{content} ✓

### Example 2 — Medium

{content} ✓

### Example 3 — Long

{content} ✓

---

## Anti-Examples

❌ WRONG: {bad example}
   Why: {specific violation}
   ✓ RIGHT: {corrected version}

---

## Color & Typography

{If applicable — see structure above}

---

## Channel Adaptations

{Table of channel-specific rules}
```

---

## Done Checklist

Before declaring complete:

- [ ] Voice dimensions scored (with provisional flag if needed)
- [ ] Vocabulary lists populated (use and ban lists)
- [ ] 3 real content examples that demonstrate the voice
- [ ] 2 anti-examples with specific violations and fixes
- [ ] Channel adaptations defined
- [ ] Color/typography sections added (if applicable)
- [ ] File saved to correct location (default: `BRAND.md`)
- [ ] File is valid markdown

---

## Cross-Skill Orchestration

**Called by:**
- `repo-bootstrap` — if no brand file exists
- User directly — for brand refresh

**Feeds into:**
- `prompt-author` — all prompts reference brand voice
- `bento-layout-director` — visual brand rules inform layout
- `lightrains-blog-writing` (if used) — brand voice in content

**Depends on:**
- `repo-bootstrap` — must have a valid folder structure first

---

## Edge Cases

| Situation | Handling |
|-----------|----------|
| User provides only website URL | Analyze the homepage and about page for voice signals |
| User says "just make something up" | Default to "technical + direct" persona, mark as provisional |
| Brand already exists | Verify accuracy, suggest updates if outdated |
| Conflicting voice samples | Ask user to pick primary direction: "Which feels more right?" |
| User wants visual-only brand file | Still include voice dimensions — visuals and tone must align |
| Industry requires compliance | Add compliance constraints (no claims, required disclaimers, etc.) |

---

## Appendix A — Standard Ban List

These phrases are banned in almost every brand. Add to the negative vocabulary list:

- "cutting-edge", "best-in-class", "industry-leading"
- "seamless", "seamlessly", "effortless"
- "leverage", "utilize", "utilization"
- "robust", "comprehensive", "holistic"
- "robust", "comprehensive", "holistic"
- "delve", "delve into", "delve deeper"
- "landscape" (as buzzword)
- "navigate" (as metaphor)
- "foster", "facilitate", "ensure"
- "excited to announce", "thrilled to share"
- "game-changing", "revolutionary"
- "powerful", "ultimate", "perfect"
- "at its core", "fundamentally"
- "In this article, we will explore..."
- "It's worth noting that..."
- "Needless to say..."
- "That being said..."
- "Without further ado..."

Add industry-specific terms as needed.