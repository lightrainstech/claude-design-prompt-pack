---
name: prompt-author
description: Write, refine, and optimize reusable prompts for bento grids, mockups, and workflows. Triggers: "write the master prompt", "draft the homepage prompt", "make a revision prompt", "create a prompt", "write a prompt for".
---

# Prompt Author

Creates high-quality, reusable prompts for AI workflows. This is the core skill — everything else (layouts, exports) flows from prompts.

## When to Use

**Trigger phrases (exact match):**
- "write the master prompt"
- "draft the homepage prompt"
- "make a revision prompt"
- "create a prompt"
- "write a prompt for"
- "compose a prompt"
- "author a prompt"
- "generate a prompt"

**Also triggers if:**
- User describes a task and says "what prompt would do this?"
- User needs a prompt rewritten or optimized
- User says "this prompt isn't working, fix it"

**Not a trigger if:**
- User provides a prompt and says "run this" (that's execution, not authoring)
- User asks for the output the prompt would produce (that's generation, not authoring)

---

## Before Starting

Ask (or infer) these:

1. **Deliverable type:** Image prompt, text prompt, or workflow prompt?
2. **Subject:** What is the prompt about?
3. **Audience:** Who will use this prompt? (affects complexity and specificity)
4. **Platform:** Which AI will run this? (Claude, Midjourney, DALL-E, GPT-4, etc.)
   - This affects syntax and constraints
5. **Format:** Single prompt or template with variables?
6. **Brand file:** Is there a BRAND.md to reference? (if not, use defaults)

**Default if not specified:**
- Type: text prompt (most common)
- Platform: Claude (default for opencode)
- Format: single prompt (no variables)
- Brand: technical + direct

---

## Prompt Types and Anatomy

### Type 1: Image Generation Prompt

**Anatomy:**
```
[Subject] + [Style] + [Composition] + [Technical specs] + [Mood/Atmosphere]
```

**Example:**
```
A modern SaaS dashboard interface, clean minimal design, light mode,
showing data visualization with line charts and bar graphs,
8K resolution, soft shadows, Figma-style UI design,
professional corporate aesthetic, morning light, screenshot quality
```

**Platform-specific syntax:**

| Platform | Syntax notes |
|----------|--------------|
| Midjourney | Use `--ar` for aspect ratio, `--style` for style codes |
| DALL-E 3 | Natural language, no special syntax needed |
| Stable Diffusion | Use权重 weights (1.0), negative prompts for exclusions |

---

### Type 2: Text Generation Prompt

**Anatomy:**
```
[Role/Identity] + [Context] + [Task] + [Constraints] + [Output format] + [Tone]
```

**Template:**
```
You are a {role} with expertise in {domain}.
{Context: what the user already knows, what situation they're in}
{Task: what they need you to produce}
{Constraints: what to avoid, what must be included}
{Output format: how to structure the response}
{Tone: how to sound}
```

**Example (blog post intro):**
```
You are a senior engineer writing for a technical blog.
The reader is a fellow engineer evaluating whether to adopt a new library.
Write the first 3 paragraphs of a blog post about {topic}.
Start with a concrete problem, not a generic introduction.
No corporate language. Use "we" for Lightrains perspective.
Include one specific example with real metrics.
End with a hook that makes the reader want the next section.
```

---

### Type 3: Workflow Prompt (Chain of Tasks)

**Anatomy:**
```
[Goal] + [Steps] + [Inputs] + [Outputs] + [Error handling]
```

**Example:**
```
Create a workflow that:
1. Takes a topic as input
2. Generates 3 related subtopics
3. For each subtopic, writes one paragraph
4. Combines into a coherent article
5. Outputs in markdown with ## headings

Inputs: {topic}
Outputs: {markdown article}
On failure: retry step, log error, continue if unsolvable
```

---

## Step-by-Step Process

### Step 1: Identify Prompt Type

Match the request to one of the three types:

| Request | Type |
|---------|------|
| "I need a prompt for a hero image" | Image |
| "Write a prompt for generating blog outlines" | Text |
| "Create a prompt that does X, then Y, then Z" | Workflow |
| Ambiguous | Ask: "Is this generating an image, text, or a multi-step process?" |

---

### Step 2: Extract Key Information

Ask (or infer) these for every prompt:

**Required:**
- What is the output? (image, text, action)
- Who is the audience?
- What is the context/situation?
- What must the output include?
- What must the output exclude?

**Nice to have:**
- Brand rules (from BRAND.md)
- Platform constraints
- Example of ideal output
- Anti-example of what to avoid

---

### Step 3: Draft the Prompt

**Follow this structure (in order):**

1. **Role assignment** (if applicable)
   - Who is the AI acting as?
   - What expertise does it have?

2. **Context provision**
   - What situation are we in?
   - What does the user already know?

3. **Task statement**
   - What needs to be produced?
   - Use action verbs: "write", "generate", "create", "analyze"

4. **Constraints**
   - What to avoid (negative constraints)
   - What must be included (positive constraints)
   - Any rules or guardrails

5. **Output format**
   - Structure: markdown, JSON, list, paragraph
   - Length: short, medium, long
   - Any required elements

6. **Tone guidance**
   - How should it sound?
   - Any voice rules from brand file

**Write prompts as if giving instructions to a capable junior — specific but not condescending.**

---

### Step 4: Optimize for Platform

**Claude-specific optimizations:**
- Use XML tags for structure: `<context>`, `<task>`, `<output>`
- Break complex tasks into numbered steps
- Include "think step by step" for reasoning tasks
- Add output validation instructions

**Midjourney-specific optimizations:**
- Start with subject
- End with style descriptors
- Use artist names for style references
- Include aspect ratio

**DALL-E specific optimizations:**
- Natural language, conversational
- Can include more detail than other platforms
- Avoid negative prompts (not supported)

---

### Step 5: Add Variables (if template)

For reusable prompts, add variables:

**Variable syntax:**
```
{variable_name}
```

**Example:**
```
Write a blog post intro about {topic}
for {audience}
in {tone} tone
```

**Variable types:**
| Type | Example | Notes |
|------|---------|-------|
| String | `{topic}` | Most common |
| Number | `{count}` | For iterations |
| Enum | `{format: json/markdown}` | Limited options |
| Boolean | `{include_examples: true}` | Binary choices |

---

### Step 6: Test the Prompt

**For text prompts:**
Run the prompt and evaluate:
- Does it produce what was requested?
- Are constraints respected?
- Is the format correct?
- Is the tone appropriate?

**For image prompts:**
Visualize mentally or run through:
- Are style descriptors coherent?
- Is composition clear?
- Are technical specs reasonable?

**For workflow prompts:**
Trace through each step:
- Are dependencies correct?
- Can any step fail silently?
- Is the final output what's expected?

---

### Step 7: Iterate Based on Test

**Common fixes:**

| Problem | Fix |
|---------|-----|
| Too vague | Add specific constraints or examples |
| Too rigid | Remove unnecessary constraints |
| Wrong tone | Add tone guidance or reference brand file |
| Missing edge cases | Add conditional logic or error handling |
| Output wrong format | Add explicit format instructions |

---

## Output Formats

### Single Prompt File

Save as `prompts/{name}.md`:

```markdown
# {Prompt Name}

**Type:** {image/text/workflow}
**Platform:** {platform}
**Author:** {your name or 'agent'}

---

{Prompt text here}

---

## Variables

| Variable | Type | Description | Default |
|----------|------|-------------|---------|
| `{var1}` | string | What this controls | - |

## Example Usage

```
{Example with variables filled in}
```

## Notes

{Any caveats, tips, or context}
```

---

### Prompt Collection File

For multiple related prompts, use a collection:

```markdown
# {Collection Name}

## Prompts

### {Prompt 1}
...content...

### {Prompt 2}
...content...

---

## Usage Guide

{How to use these prompts together}
```

---

## Quality Rubric

Rate each prompt on these dimensions:

| Dimension | Score | Criteria |
|-----------|-------|----------|
| **Clarity** | 1-5 | Does the prompt say exactly what it wants? No ambiguity? |
| **Specificity** | 1-5 | Are constraints concrete, not vague? |
| **Completeness** | 1-5 | Does it include all needed context, format, and constraints? |
| **Correctness** | 1-5 | Is it syntactically correct for the target platform? |
| **Reusability** | 1-5 | Are variables clearly named? Is it templated appropriately? |

**Minimum passing scores:**
- Clarity: 4+
- Completeness: 4+
- All others: 3+

**If any score is below minimum:**
- Identify the specific problem
- Fix it
- Retest

---

## Common Pitfalls and Fixes

### Pitfall 1: Vague Role Assignment

**Bad:**
```
You are a writer.
```

**Good:**
```
You are a senior backend engineer with 10 years of experience in distributed systems.
You have debugged production incidents at scale and understand operational trade-offs.
```

### Pitfall 2: Missing Output Format

**Bad:**
```
Write about microservices.
```

**Good:**
```
Write a 2-paragraph explanation of microservices architecture.
Format:
- Paragraph 1: What it is (1 sentence) + why it matters (2 sentences)
- Paragraph 2: Main benefit (1 sentence) + trade-off (2 sentences)
```

### Pitfall 3: Conflicting Constraints

**Bad:**
```
Write something short but comprehensive.
```

**Fix:**
```
Write exactly 3 sentences that cover the 3 most important points.
Prioritize: clarity > completeness > length.
```

### Pitfall 4: Platform Mismatch

**Bad for Claude (too verbose):**
```
As a language model with extensive training data, I would like you to please
provide a detailed response regarding the topic of...
```

**Good for Claude:**
```
Provide a detailed response about {topic}.
Include: key points, examples, and a conclusion.
```

### Pitfall 5: Variables Too Broad

**Bad:**
```
Write about {subject}.
```

**Good:**
```
Write a 200-word introduction about {topic} for {audience}.
Focus on {angle}: practical benefits, not theory.
```

---

## Before/After Examples

### Example 1: Image Prompt

**Before:**
```
Dashboard design for a SaaS app.
```

**After:**
```
A modern SaaS analytics dashboard, dark mode, featuring:
- Line chart showing 30-day user growth (upward trend)
- Bar chart showing revenue by plan (3 bars)
- KPI cards with percentage changes (+12%, +8%, -3%)
- User avatar cluster showing recent signups

Style: Clean Figma interface, soft shadows, subtle gradients
Colors: Dark navy background (#0F172A), white text, accent blue (#3B82F6)
Layout: Left sidebar (collapsed), main content area with 2-column grid
Quality: 8K, photorealistic, screenshot aesthetic
Mood: Professional, data-driven, confident
```

---

### Example 2: Text Prompt

**Before:**
```
Write a blog post intro.
```

**After:**
```
Write the opening 3 paragraphs of a technical blog post.

Role: Senior engineer writing for peers
Audience: Developers evaluating a new tool or approach
Opening: Start with a specific problem, not a generic observation
Structure:
  - Paragraph 1: The problem (concrete, not abstract)
  - Paragraph 2: Why common solutions fail (specific reasons)
  - Paragraph 3: What we're about to show (the hook)

Constraints:
  - No "In this article..."
  - No corporate language
  - One specific example with metrics if possible
  - End with a question or challenge to the reader

Format: Markdown, ~200 words total
```

---

### Example 3: Workflow Prompt

**Before:**
```
Generate content for a landing page.
```

**After:**
```
Create a landing page copy workflow that:

1. INPUT: {product_name}, {target_audience}, {primary_benefit}

2. Generate headlines (5 options):
   - Pattern A: Problem-first
   - Pattern B: Benefit-first
   - Pattern C: Question-based
   - Pattern D: Bold claim
   - Pattern E: WRYDWTD (What Race You Want to Die Doing)

3. For each headline, generate:
   - Subheadline (1 sentence)
   - 3 bullet points (benefit-focused)
   - CTA text (action-oriented, max 5 words)

4. OUTPUT FORMAT:
   ## Headline A: {headline}
   Subheadline: {text}
   Bullets:
   - {bullet 1}
   - {bullet 2}
   - {bullet 3}
   CTA: {text}

5. ERROR HANDLING:
   - If input missing: ask for {product_name} at minimum
   - If output too long: trim bullets to 2
   - If tone off: regenerate with "more {adjective}" instruction
```

---

## Done Checklist

Before declaring complete:

- [ ] Prompt type identified
- [ ] Key information extracted (output, audience, constraints)
- [ ] Prompt drafted following anatomy template
- [ ] Optimized for target platform
- [ ] Variables defined (if template)
- [ ] Tested or mentally traced
- [ ] Iterated based on test results
- [ ] Saved to correct location (`prompts/{name}.md` or skill file)
- [ ] Quality rubric scores all pass minimums
- [ ] Example usage provided
- [ ] Notes/caveats documented

---

## Cross-Skill Orchestration

**Called by:**
- User directly
- `repo-bootstrap` — if skills need prompts written
- `bento-layout-director` — for prompt templates

**Feeds into:**
- `bento-layout-director` — image prompts become layout concepts
- `packaging-and-export` — prompts are packaged as deliverables
- `repo-bootstrap` — prompts can be part of skill definitions

**Depends on:**
- `brand-system-builder` — for tone guidance (if brand file exists)

---

## Edge Cases

| Situation | Handling |
|-----------|----------|
| Request is ambiguous | Ask one clarifying question: "Is this for images, text, or a workflow?" |
| User provides example output | Reverse-engineer the prompt from the example |
| Platform not specified | Default to Claude syntax, note the assumption |
| Prompt works but feels weak | Add specificity — more constraints, better examples |
| Multiple valid approaches | Show both, let user pick, explain trade-offs |
| User says "this isn't working" | Diagnose: wrong type? Missing constraints? Platform mismatch? |
| Prompt needs iteration | Show before/after, explain the improvement |