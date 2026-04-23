---
name: bento-layout-director
description: Convert ideas into modular bento-grid UI concepts and visual layouts. Triggers: "make it bento", "arrange in tiles", "turn this into a block UI", "create bento layout", "design grid layout", "plan the grid".
---

# Bento Layout Director

Transforms content concepts into structured bento-grid layouts — modular card systems that balance visual hierarchy, information density, and breathing room.

## When to Use

**Trigger phrases (exact match):**
- "make it bento"
- "arrange in tiles"
- "turn this into a block UI"
- "create bento layout"
- "design grid layout"
- "plan the grid"
- "visual layout"
- "tile arrangement"
- "grid composition"
- "card layout"

**Also triggers if:**
- User describes content and asks "how should this look?"
- User says "I have a lot of content, how do I organize it visually?"
- `prompt-author` outputs image prompts that need layout direction

**Not a trigger if:**
- User asks for code implementation (that's development, not design)
- User asks for CSS/HTML (that's execution, not layout planning)
- User wants a wireframe specifically (this is visual composition, not technical wireframes)

---

## Before Starting

Ask (or infer) these:

1. **Content type:** What content needs to be arranged? (features, stats, steps, team, products, etc.)
2. **Layout intent:** What should the viewer do/feel? (compare, discover, understand, navigate)
3. **Density:** How much content? (3 items, 6 items, 12+ items)
4. **Focal point:** Is one thing more important than others? (hero vs. equal)
5. **Platform:** Where will this live? (web, mobile, presentation, social)
6. **Brand file:** Is there a BRAND.md to reference? (colors, spacing, typography)

**Default if not specified:**
- Items: 4-6 (most common)
- Density: medium (not sparse, not cramped)
- Focal point: equal (bento grids work best with peer items)
- Platform: web (responsive baseline)

---

## Bento Grid Principles

### Core Philosophy

Bento grids are named after Japanese lunch boxes (bento) — a single container with compartments of different sizes, arranged intentionally.

**Key principles:**

1. **Varied sizes create hierarchy** — Big tiles = important. Small tiles = supporting.
2. **White space is content** — Empty space lets the eye rest and emphasizes what remains.
3. **Alignment beats randomness** — Everything snaps to an invisible grid.
4. **Breathing room is non-negotiable** — Elements too close feel cramped; elements too far feel disconnected.
5. **Color guides attention** — Use brand colors strategically, not everywhere.

### Grid Anatomy

```
┌─────────────────────────────────────────────┐
│                 CONTAINER                    │
│  ┌───────────┬───────────┬───────────────┐  │
│  │           │           │               │  │
│  │   TILE    │   TILE    │    TILE        │  │
│  │   (2x2)   │   (1x2)   │    (2x2)       │  │
│  │           │           │               │  │
│  ├───────────┼───────────┼───────────────┤  │
│  │           │           │               │  │
│  │   TILE    │   TILE    │    TILE        │  │
│  │   (1x1)   │   (1x1)   │    (1x1)       │  │
│  │           │           │               │  │
│  └───────────┴───────────┴───────────────┘  │
│                                             │
│  ← SPACING (gutter) between tiles          │
│  ← PADDING around container                 │
└─────────────────────────────────────────────┘
```

---

## Tile Sizes and When to Use

### Standard Tile Sizes (12-column grid)

| Size | Columns | Rows | When to use |
|------|---------|------|-------------|
| **Hero** | 8 | 3 | One dominant item that deserves focus |
| **Large** | 6 | 2 | Important item, paired with equal peer |
| **Medium** | 4 | 2 | Standard item, most common size |
| **Small** | 3 | 1 | Secondary item, can be grouped |
| **Micro** | 2 | 1 | Tertiary item, metadata, icons |

### Size Patterns

**Pattern A — Equal Grid (all tiles same size)**
```
┌───┬───┬───┐
│   │   │   │
├───┼───┼───┤
│   │   │   │
├───┼───┼───┤
│   │   │   │
└───┴───┴───┘
```
Use when: All items have equal importance. Pure comparison.

**Pattern B — Hero + Supporting (one dominant)**
```
┌─────────────┐
│             │
│    HERO     │
│    (2x2)    │
│             │
├─────┬───┬───┤
│     │   │   │
└─────┴───┴───┘
```
Use when: One thing is clearly more important. Landing page, feature highlight.

**Pattern C — Asymmetric Row (varied widths)**
```
┌───────────┬───┐
│           │   │
│    2/3    │1/3│
│           ├───┤
│           │   │
├─────┬─────┤   │
│ 1/3 │ 1/3 │   │
├─────┴─────┼───┤
│    2/3    │1/3│
└───────────┴───┘
```
Use when: Need visual rhythm. Items naturally group into categories.

**Pattern D — Brick / Mosaic**
```
┌─────┬───────┐
│     │       │
│ 1/2 │  1/2  │
├─────┼───────┤
│     │       │
│1/4  │  1/4  │ + 1/4 + 1/4 on next row...
```
Use when: Many small items. Gallery, feature grid, team section.

---

## Step-by-Step Process

### Step 1: Audit the Content

List every piece of content that needs a tile:

| Item | Importance | Size hint |
|------|------------|-----------|
| Feature A | High | Large |
| Feature B | Medium | Medium |
| Feature C | Medium | Medium |
| Stat 1 | Low | Small |
| Stat 2 | Low | Small |

**Rules:**
- If fewer than 3 items: consider a single-column stack instead
- If more than 12 items: group into categories first

---

### Step 2: Define Hierarchy

**Decision tree:**

```
Is one item more important than all others?
│
├── YES → Hero + Supporting pattern
│        - Hero gets largest tile (8 or 6 cols)
│        - Others fill remaining space
│
└── NO → Equal Grid or Asymmetric pattern
         - All tiles similar size, OR
         - Tiles vary by content type (e.g., images larger than text)
```

---

### Step 3: Select Grid System

**12-column grid (default):**
- Most flexible
- Good for: web layouts, presentations, complex arrangements

**6-column grid:**
- Simpler math (halves, thirds)
- Good for: mobile, simpler compositions

**4-column grid:**
- Classic 2x2 or 1x4
- Good for: social media, simple feature lists

---

### Step 4: Assign Tile Sizes

**Size formula:**
- Total columns in row = 12 (or 6, 4)
- Tiles in row must sum to grid total

**Common valid combinations:**

| Grid | Valid combinations |
|------|---------------------|
| 12-col | 6+6, 4+4+4, 4+8, 3+3+3+3, 8+4, 3+9 |
| 6-col | 3+3, 2+2+2, 4+2, 2+4 |
| 4-col | 2+2, 1+1+1+1, 3+1 |

---

### Step 5: Define Spacing

**Spacing scale (use this, not random numbers):**

| Token | Pixels | Use when |
|-------|--------|----------|
| `xs` | 4px | Between tightly related elements |
| `sm` | 8px | Between elements in same group |
| `md` | 16px | Between tiles in bento grid |
| `lg` | 24px | Between groups of tiles |
| `xl` | 32px | Section padding |
| `xxl` | 48px | Page margins on large screens |

**Standard bento grid spacing:**
- Gutter (between tiles): `md` (16px)
- Container padding: `lg` or `xl` (24-32px)
- Corner radius on tiles: `md` (8px) — consistent across all tiles

---

### Step 6: Define Visual Treatment

**For each tile, specify:**

```
┌────────────────────────────┐
│                            │
│  [Label / Category]        │
│                            │
│  [Main visual or title]    │
│                            │
│  [Supporting text or stat] │
│                            │
│  [Optional: CTA or link]   │
│                            │
└────────────────────────────┘
```

| Element | Rules |
|---------|-------|
| **Label** | Uppercase, small, brand accent color |
| **Title** | Bold, larger, readable at a glance |
| **Visual** | Image, icon, chart, diagram — clear at small size |
| **Description** | 1-3 lines max. No paragraphs. |
| **CTA** | Optional. One line, action-oriented. |

---

### Step 7: Specify Color Usage

**Decision tree:**

```
Is this a highlighted/featured tile?
│
├── YES → Use brand primary color (background or border)
│
└── NO → Neutral background (light gray or white)
         Use brand color only for labels/icons
```

**Color rules:**
- Maximum 2-3 colors per layout
- One dominant (background), one accent (labels/links), one neutral (text)
- No tile should have more than 2 colors

---

## Output Format

### ASCII Layout Diagram (Primary Output)

```
┌─────────────────────────────────────────────────────────────┐
│                      {Section Title}                         │
│                                                             │
│  ┌──────────────────────┐  ┌────────┐  ┌────────────────┐  │
│  │                      │  │        │  │                │  │
│  │    {Large Tile}      │  │ {Med}  │  │   {Large Tile} │  │
│  │                      │  │        │  │                │  │
│  │                      │  ├────────┤  │                │  │
│  │                      │  │ {Sm}   │  │                │  │
│  ├──────────┬───────────┤  ├────────┤  ├────────────────┤  │
│  │  {Med}   │  {Med}    │  │ {Med}  │  │    {Med}       │  │
│  │          │           │  │        │  │                │  │
│  │          │           │  │        │  │                │  │
│  └──────────┴───────────┘  └────────┘  └────────────────┘  │
│                                                             │
│  Spacing: md (16px gutters)  •  Radius: md (8px)           │
└─────────────────────────────────────────────────────────────┘
```

### Layout Spec (Structured)

```markdown
## Layout: {Name}

**Grid:** 12-column
**Pattern:** {A/B/C/D from above}
**Gutter:** 16px
**Radius:** 8px

### Tiles

| Tile | Position | Size | Content |
|------|----------|------|---------|
| Hero | Row 1 | 8 cols | {description} |
| Med 1 | Row 1 | 4 cols | {description} |
| Med 2 | Row 2 | 4 cols | {description} |
| ... | ... | ... | ... |

### Color Rules
- Background: #F8FAFC (neutral)
- Hero tile: #0F172A (dark, white text)
- Labels: #3B82F6 (accent)
- Body text: #334155

### Typography
- Title: Bold, 24px
- Label: Uppercase, 12px, tracking wide
- Body: Regular, 14px
```

---

## Common Layout Recipes

### Recipe 1: 4-Feature Equal Grid

```
┌────────┬────────┐
│        │        │
│ Feat 1 │ Feat 2 │
│        │        │
├────────┼────────┤
│        │        │
│ Feat 3 │ Feat 4 │
│        │        │
└────────┴────────┘
```
- All equal size
- Icon + title + short description
- Use when: 4 features, all equal importance

### Recipe 2: Hero + 4 Grid

```
┌────────────────┐
│                │
│     HERO       │
│    (centered)  │
│                │
├──────┬────┬───┤
│      │    │   │
└──────┴────┴───┘
```
- Hero is 12 cols
- Supporting items fill 3 columns each below
- Use when: One dominant feature, 3 supporting points

### Recipe 3: Stats Row

```
┌────────┬────────┬────────┬────────┐
│  $2.4M │   94%  │  12ms  │  4.9★  │
│ revenue │  uptime │ latency│ rating │
└────────┴────────┴────────┴────────┘
```
- 4 equal tiles, horizontal
- Big number + small label
- Use when: Showing metrics or achievements

### Recipe 4: Timeline or Steps

```
┌────────┐
│ Step 1 │───→┌────────┐
│        │    │ Step 2 │
└────────┘    └────────┘
     │             │
     ↓             ↓
┌────────┐    ┌────────┐
│ Step 3 │───→│ Step 4 │
│        │    │        │
└────────┘    └────────┘
```
- Sequential flow
- Shows progression
- Use when: Process, journey, onboarding

### Recipe 5: Team or Profile Grid

```
┌─────┬─────┬─────┬─────┐
│ 👤  │ 👤  │ 👤  │ 👤  │
│     │     │     │     │
├─────┼─────┼─────┼─────┤
│ 👤  │ 👤  │ 👤  │     │
│     │     │     │ +N  │
└─────┴─────┴─────┴─────┘
```
- Equal tiles for each person
- Photo + name + role
- Use when: Team, testimonials, case studies

---

## Annotated Examples

### Example 1: Good Bento Grid

```
┌────────────────────────────────────────────────┐
│           OUR CAPABILITIES                     │
│                                                │
│  ┌─────────────────────────┐  ┌────────────┐   │
│  │  🚀                     │  │  🎯        │   │
│  │  Fast Deployment       │  │  Precision │   │
│  │  Ship in hours, not    │  │  99.9%     │   │
│  │  days.                 │  │  accuracy. │   │
│  │                        │  │            │   │
│  └─────────────────────────┘  └────────────┘   │
│                                                │
│  ┌────────────┐  ┌─────────────────────────┐   │
│  │  🔒        │  │  📊                     │   │
│  │  Secure    │  │  Scalable               │   │
│  │  Enterprise-│  │  From prototype to     │   │
│  │  grade.     │  │  production at scale.  │   │
│  └────────────┘  └─────────────────────────┘   │
│                                                │
│  ✓ Equal visual weight   ✓ Consistent spacing │
│  ✓ Clear hierarchy via icon/size ✓ Readable    │
└────────────────────────────────────────────────┘
```

### Example 2: Bad Bento Grid (and why)

```
┌────────────────────────────────────────────────┐
│           OUR CAPABILITIES                     │
│                                                │
│  ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐  │
│  │ feat │ │ feat │ │ feat │ │ feat │ │ feat │  │
│  └──────┘ └──────┘ └──────┘ └──────┘ └──────┘  │
│                                                │
│  ✗ Too many items (5 in a row)                │
│  ✗ No visual hierarchy                        │
│  ✗ No breathing room                         │
│  ✗ Text too small to read                     │
└────────────────────────────────────────────────┘
```

**Fix:** Reduce to 4 items max. Use 2x2 grid. Add more spacing.

---

## Done Checklist

Before declaring complete:

- [ ] All content items have a tile assigned
- [ ] Hierarchy is clear (sizes reflect importance)
- [ ] Grid totals are valid (columns sum correctly)
- [ ] Spacing is consistent (using spacing scale)
- [ ] Color usage is restrained (max 2-3 colors)
- [ ] Each tile has required elements (title, description, optional visual)
- [ ] Layout spec is documented in output
- [ ] ASCII diagram is provided
- [ ] Platform considerations noted (web/mobile differences)

---

## Cross-Skill Orchestration

**Called by:**
- User directly
- `prompt-author` — when generating image prompts that need layout

**Feeds into:**
- `packaging-and-export` — layout specs become part of deliverables
- `prompt-author` — layout informs what the image prompt should describe

**Depends on:**
- `brand-system-builder` — for color palette and typography rules
- `prompt-author` — for content to arrange

---

## Edge Cases

| Situation | Handling |
|-----------|----------|
| Uneven number of items | Leave one tile empty or use it for whitespace — don't force fit |
| Items have very different content types | Consider separate sections (stats row + feature grid) |
| Very long text in a tile | Truncate to 3 lines, link to full content |
| Mobile consideration | Design desktop first, then specify how to adapt (stack vertically, combine tiles) |
| Dark mode needed | Specify colors for both light and dark variants |
| No brand file | Use defaults: neutral grays, blue accent, sans-serif typography |