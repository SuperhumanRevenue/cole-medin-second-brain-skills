---
name: plugin-design-report
description: |
  Analyze a user's workflows and generate a personalized Plugin Design Report as an interactive React artifact. Use when the user wants to identify plugin opportunities, get a plugin optimization audit, or generate comprehensive plugin blueprints for their workflows.

  TRIGGERS - Use this skill when user says:
  - "analyze my plugins" / "plugin design report" / "plugin audit"
  - "what plugins should I build" / "plugin opportunities"
  - "generate plugin blueprints" / "design my plugins"
  - "plugin optimization report" / "audit my workflow for plugins"
  - Any request about identifying, designing, or planning software plugins based on workflow analysis

  Creates an interactive React artifact with plugin scoring, categorization, and copy-ready build prompts for entire plugin architectures.
---

# Plugin Design Report

Generate a personalized Plugin Design Report as an interactive React artifact. This skill audits the user's workflows and identifies opportunities to build entire software plugins — complete with architecture, tech stack, APIs, database schemas, and deployment strategy.

## Process Overview

1. **Audit** — Analyze user's workflows and identify plugin opportunities
2. **Score & Categorize** — Rate and classify each plugin opportunity
3. **Build the Report** — Generate the interactive React artifact

---

## Step 1: Audit the User's Workflows

Review everything known about the user from memory and conversation context. Identify:

- **Repeated workflows** (daily/weekly) that could be automated by a plugin
- **Manual integrations** where the user bridges two or more tools by hand
- **Data pipelines** that are fragile, manual, or missing entirely
- **Collaboration pain points** where a plugin could streamline team workflows
- **Industry-specific gaps** — plugins that exist for their industry but they haven't adopted

If context is thin, ask:

> "I don't have enough context yet. Tell me:
> 1. Your role and industry
> 2. Your top 5 recurring tasks
> 3. What tools/platforms you use daily
> 4. What frustrates you most about your current workflow
> 5. Any integrations you wish existed"

Proceed only after gathering sufficient context.

---

## Step 2: Score & Categorize

Categorize each plugin opportunity into exactly one of:

| Category | Definition | Color |
|----------|-----------|-------|
| **Optimized** | User already has this plugin or a structured solution in place | Green (#059669 text, #10b981 dot) |
| **Identified** | User does this regularly but has no plugin — clear build candidate | Amber (#d97706 text, #f59e0b dot) |
| **Untapped** | User should be doing this based on role/industry but isn't | Red (#dc2626 text, #ef4444 dot) |

**Rules:**
- Only include genuinely repeatable, high-value plugin opportunities
- Aim for 5–9 total plugins
- Be specific to the user's actual workflow — no generic suggestions
- Each plugin must have a clear architecture type (see `references/plugin-archetypes.md`)

---

## Step 3: Build the Interactive Report

Create a **React artifact** that follows this exact specification.

### Design System

| Token | Value |
|-------|-------|
| Page background | `#f8f9fc` |
| Card background | `#ffffff` with `1px solid #e2e8f0` border |
| Body font | Google Fonts — **Inter** |
| Label/badge font | Google Fonts — **JetBrains Mono** |
| Primary color | Indigo `#6366f1` |
| Text dark | `#1e293b` |
| Text muted | `#64748b` |
| Border radius | `12px` cards, `9999px` pills |
| Shadow | `0 1px 3px rgba(0,0,0,0.06), 0 1px 2px rgba(0,0,0,0.04)` |

Category colors:

| Category | Text | Dot/Border |
|----------|------|------------|
| Optimized | `#059669` | `#10b981` |
| Identified | `#d97706` | `#f59e0b` |
| Untapped | `#dc2626` | `#ef4444` |

### Layout (top to bottom)

#### 1. Header

- `"PLUGIN DESIGN REPORT"` label — JetBrains Mono, uppercase, small, indigo
- `"Your Plugin Design Report"` — h1, dark
- Subtitle: `"Based on your workflow patterns and integration analysis"`

#### 2. Score Dashboard

Dark indigo gradient background: `#1e1b4b → #312e81 → #3730a3`

- **Left**: SVG circular progress ring (120×120) showing optimization percentage with animated `stroke-dashoffset`
- **Right**:
  - `"Plugin Optimization Score"` label
  - `"X of Y plugins optimized"` headline
  - Description text summarizing the user's plugin maturity
  - Legend showing Optimized / Identified / Untapped counts with colored dots
- **Score formula**: `(optimized count / total count) × 100`

#### 3. Personalized Plugin Commentary

White card with subtle shadow. Three sections:

- **Your Strengths** (green badge): 2–3 sentences on what the user has already automated well. Reference specific plugins or tools they use.
- **Opportunities** (amber badge): 2–3 sentences on their biggest gaps. Include estimated impact where possible (e.g., "~5 hours/week in manual data entry").
- **Bottom Line** (bold, accent color with ⚡ icon): One sentence naming the single highest-impact plugin to build first and why.

This commentary should read like a consultant reviewing their setup — specific, actionable, not generic.

#### 4. Instruction Banner

Light indigo background with 💡 icon:

> "Click **Design →** to answer quick questions about your requirements, then copy a ready-made prompt. Paste it into a new Claude chat to get a complete plugin blueprint with architecture, code structure, and deployment plan."

#### 5. Plugin Cards (one per opportunity)

Each card contains:

- **Category badge** — small pill with colored text/border
- **Plugin name** (bold, 17px) and description
- **Architecture tag** — small gray pill showing plugin type (e.g., "API Integration", "Chrome Extension", "CLI Tool", "Full-Stack App", "Webhook Pipeline", "Browser Extension", "Desktop App", "Mobile App", "Slack Bot", "VS Code Extension")
- **"Design →"** button on the right

**When expanded** (clicking Design), show:

- `"PLUGIN CONFIGURATION"` label in JetBrains Mono
- 3–4 qualifying questions specific to that plugin with text input fields. Questions should cover:
  - **Scale/scope**: "How many users/requests do you expect?"
  - **Integrations**: "Which specific tools/APIs should this connect to?"
  - **Tech preferences**: "Any preferred language or framework?"
  - **Deployment**: "Where should this run? (cloud, local, browser, etc.)"
- A **"📋 Copy Blueprint Prompt"** button that:
  - Generates a complete prompt to build the full plugin (architecture, code, deployment)
  - Incorporates the user's answers to the qualifying questions
  - On click: copies to clipboard and changes to `"✓ Copied! Paste into Claude →"` (green) for 3 seconds
- Helper text: `"Works without answers too — but answers produce a more targeted blueprint"`

**Only one card can be expanded at a time.**

#### 6. Footer

> "Plugins are ranked by estimated weekly impact. Build the top-scoring ones first for maximum ROI."

### Data Structure

```js
{
  id: string,
  name: string,
  description: string,
  category: "optimized" | "identified" | "untapped",
  architectureType: string,  // e.g. "API Integration", "CLI Tool", "Full-Stack App"
  questions: [{ id: string, text: string, answer: string }]
}
```

Use `useState` for expansion state and per-card answer state.

### Build Prompt Generation

When the user clicks **"Copy Blueprint Prompt"**, the copied text must follow the template in `references/build-prompt-template.md`. Read that file to construct the prompt.

The generated prompt should instruct Claude to produce a complete plugin implementation plan covering:

1. Architecture overview and system design
2. Tech stack with justifications
3. Project structure (directory tree)
4. Database schema (if applicable)
5. API endpoints or interface definitions
6. Core module implementations
7. Authentication and authorization (if applicable)
8. Error handling and logging strategy
9. Testing strategy
10. Deployment and CI/CD configuration
11. Environment variables and configuration
12. Step-by-step build order

---

## Plugin Archetypes Reference

When categorizing plugins, consult `references/plugin-archetypes.md` for common architecture patterns and their typical tech stacks. Use this to assign the `architectureType` field and tailor qualifying questions.

---

## Quality Checklist

Before generating the artifact:

- [ ] At least 5 plugin opportunities identified
- [ ] Each plugin has a clear, specific name (not generic)
- [ ] Each plugin has a concrete description tied to user's workflow
- [ ] Category assignments are justified
- [ ] Architecture types are appropriate for each plugin's scope
- [ ] Qualifying questions are specific to each plugin (not copy-pasted)
- [ ] Commentary references the user's actual tools and workflows
- [ ] Build prompts produce actionable, complete blueprints
