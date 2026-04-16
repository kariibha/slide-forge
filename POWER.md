---
name: "Slide Forge"
displayName: "Slide Forge"
icon: "icon.svg"
description: "Generate polished Reveal.js HTML presentations from any topic. Creates infographic-style decks with glassmorphic cards, SVG charts, speaker notes, inline editing, and an interactive toolbar for adding/deleting slides and cards — all in the browser."
keywords: ["presentation", "slides", "deck", "powerpoint", "reveal", "infographic", "training", "workshop", "demo", "pitch"]
---

# Slide Forge

Generate polished Reveal.js HTML presentations with infographic-quality visuals, SVG charts, speaker notes, and interactive editing — from any topic.

## Onboarding

### Step 1: Validate MCP servers

**Included with this power:**
- `context7` — Library documentation lookup for technical topics

**Recommended (install separately):**
- Any documentation MCP relevant to your domain
- Web search is used automatically for current information

### Step 2: Add presentation review hook (optional)

Add a hook to `.kiro/hooks/review-presentation.kiro.hook`:

```json
{
  "enabled": true,
  "name": "Review Presentation Quality",
  "description": "Check generated presentation for overflow, sizing, and speaker notes",
  "version": "1",
  "when": { "type": "userTriggered" },
  "then": {
    "type": "askAgent",
    "prompt": "Review the most recently generated HTML presentation file. Check: 1) All content fits within 1280x720, 2) Every slide has speaker notes, 3) Footer bar is present, 4) No text overflow, 5) Cards are glassmorphic."
  }
}
```

## When to Load Steering Files

- Generating any presentation → `design-system.md`
- Creating SVG charts or diagrams → `chart-templates.md`
- Need icons or logos → `assets/` folder

## Bundled Assets

The `assets/` folder contains:

| File | Description |
|------|-------------|
| `assets/icon.svg` | Slide Forge power icon |

Users can add their own brand assets (logos, icons) to the `assets/` folder. The agent will reference them when generating presentations.

## Workflow

### Step 1: Understand the Request

The user may provide:
- A topic (e.g. "Create a deck about microservices architecture")
- A markdown file path
- Raw text pasted in chat
- A reference URL or document
- Brand assets or logos to include

### Step 2: Ask Clarifying Questions

Ask conversationally:

**Round 1 — Content & Audience:**
1. **Topic/Content** — What is this about?
2. **Audience** — Who is this for? (team, customers, conference, training)
3. **Tone** — Technical deep-dive, executive overview, or workshop?

**Round 2 — Branding & Style:**
4. **Theme** — Light or dark mode? (default: dark)
5. **Brand colors** — Any specific colors? (default: blue/purple gradient palette)
6. **Logo/footer** — Any logo or footer text to include?
7. **Slide count** — How many? (default: 5-8)

**Round 3 — Research:**
8. **Approval** — "Should I research this topic? I can use library docs, web search, and any MCP servers you have installed."
9. Get explicit approval before searching.

**Round 4 — Output:**
10. **Output path** — Where to save the HTML file?

### Step 3: Research (with approval)

Priority order:
1. Context7 — library/framework documentation
2. Web search — trusted sources
3. User-provided documents or URLs

### Step 4: Generate

Build complete HTML following the design system in `design-system.md`. Every deck must include:
- Footer bar with optional logo, copyright text, and slide number
- Speaker notes on every slide (SUMMARY + TRANSCRIPT format)
- **Interactive editing toolbar** — CSS and JS from `design-system.md`
- Content that fits 1280×720
- All text elements must have `contenteditable="true"`
- Cards must use glassmorphic styling

### Step 5: Verify

Check: content fits, notes present, footer visible, E key toggles edit toolbar, cards are glassmorphic.

## Interactive Editing Features

Every generated deck includes a built-in editing toolbar (press **E** to toggle):

### Slide Management
- **Add Slide** — Inserts a new slide after the current one with placeholder content and speaker notes
- **Delete Slide** — Removes the current slide and its notes (with confirmation)

### Card Management
- **Add Card** — Adds a new glassmorphic card to the current slide
- **Delete Card** — Click a card to select it (outline), then click delete
- **Edit Card** — All card text is contenteditable in edit mode

### Export
- **Save as HTML** — Downloads the edited deck as a clean HTML file

### Keyboard Shortcuts
| Key | Action |
|-----|--------|
| **E** | Toggle edit mode (toolbar + contenteditable) |
| **S** | Open speaker notes window |
| **←/→** | Navigate slides |
| **Esc** | Overview mode |

## Best Practices

### Do:
- Use the design system consistently
- Include speaker notes tailored to the audience
- Use SVG charts for data visualization (inline, no external libraries)
- Ask for brand assets (logo, colors) before generating
- Split content across slides rather than shrinking fonts

### Don't:
- Use fonts smaller than 0.5em for body text
- Pack icons with less than 10px gap
- Include proprietary data without explicit approval
- Generate more than 12 slides without asking
