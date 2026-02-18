# Build Prompt Template

When the user clicks "Copy Blueprint Prompt" on a plugin card, generate a prompt following this template. Replace all bracketed placeholders with actual values from the plugin data and the user's answers.

---

## Template

```
Design and build me a complete Claude Code plugin called "[PLUGIN NAME]".

## Overview
[PLUGIN DESCRIPTION]

## Architecture Type
[ARCHITECTURE TYPE] (e.g., API Integration, CLI Tool, Claude Code Plugin, Full-Stack Web App, etc.)

## Plugin Components Needed
[List which Claude Code plugin components this plugin requires:]
- [x/blank] Skills (skills/name/SKILL.md)
- [x/blank] Commands (commands/*.md)
- [x/blank] Agents (agents/*.md)
- [x/blank] Hooks (hooks/hooks.json)
- [x/blank] MCP Servers (.mcp.json)
- [x/blank] LSP Servers (.lsp.json)

## My Requirements
[For each answered question, include:]
- [Question text]: [User's answer]

## What I Need You to Deliver

### 1. Plugin Manifest
Create `.claude-plugin/plugin.json` with:
- name (kebab-case, used as namespace for /plugin-name:skill-name)
- version (semantic versioning: MAJOR.MINOR.PATCH, start at 1.0.0)
- description
- author (name, email, url)
- keywords (for marketplace discovery)
- Any custom component paths if not using defaults

### 2. Directory Structure
Create the complete plugin directory tree following this layout:
```
[plugin-name]/
├── .claude-plugin/
│   └── plugin.json
├── commands/           (if commands needed)
├── agents/             (if agents needed)
├── skills/             (if skills needed)
│   └── [skill-name]/
│       ├── SKILL.md
│       ├── scripts/    (if deterministic operations needed)
│       └── references/ (if context documents needed)
├── hooks/              (if hooks needed)
│   └── hooks.json
├── .mcp.json           (if MCP servers needed)
├── .lsp.json           (if LSP servers needed)
└── scripts/            (shared utility scripts)
```
IMPORTANT: Only plugin.json goes inside .claude-plugin/. All other dirs at root.

### 3. Architecture Overview
- System design diagram (text/ASCII showing component interactions)
- Data flow between components
- External service dependencies
- Key architectural decisions and trade-offs

### 4. Tech Stack
- Language and runtime with version
- Framework(s) with justification
- Database (if applicable) with schema rationale
- Key libraries and dependencies

### 5. Plugin Components (implement all that apply)

#### Skills (skills/name/SKILL.md)
For each skill, create:
- YAML frontmatter with `name` and `description` (description must include trigger conditions)
- Markdown body with instructions (keep under 500 lines)
- Progressive disclosure: metadata → body → references
- Reference files in skills/name/references/ for detailed content
- Scripts in skills/name/scripts/ for deterministic operations

#### Commands (commands/*.md)
For each command, create:
- YAML frontmatter with `description`
- Use `$ARGUMENTS` placeholder for user input
- Keep commands focused on single actions

#### Agents (agents/*.md)
For each agent, create:
- YAML frontmatter with `name` and `description`
- System prompt body describing role, expertise, and behavior

#### Hooks (hooks/hooks.json)
Configure event handlers:
- Use correct case-sensitive event names: PreToolUse, PostToolUse, PostToolUseFailure, PermissionRequest, UserPromptSubmit, Notification, Stop, SubagentStart, SubagentStop, SessionStart, SessionEnd, TeammateIdle, TaskCompleted, PreCompact
- Hook types: "command" (shell), "prompt" (LLM eval), "agent" (agentic verifier)
- Use ${CLAUDE_PLUGIN_ROOT} for all script paths
- Use matchers to target specific tools (e.g., "Write|Edit")
- Make all scripts executable with proper shebang lines

#### MCP Servers (.mcp.json)
Configure external tool connections:
- Use ${CLAUDE_PLUGIN_ROOT} for paths
- Support stdio, SSE, and streamable HTTP transports
- Include environment variable configuration

#### LSP Servers (.lsp.json)
Configure language intelligence:
- Map file extensions to language identifiers
- Document which binaries users need to install separately

### 6. Database Schema (if applicable)
- Table/collection definitions with fields, types, and constraints
- Relationships and indexes
- Migration strategy

### 7. API / Interface Design (if applicable)
- All endpoints or commands with request/response shapes
- Authentication and authorization scheme
- Rate limiting and validation rules
- Error response format

### 8. Core Implementation
- Implement main modules with full, working code
- Use ${CLAUDE_PLUGIN_ROOT} for all internal path references
- All paths must be relative starting with ./
- Follow the language/framework's idiomatic patterns
- Handle edge cases and errors

### 9. Error Handling & Logging
- Error taxonomy (expected vs unexpected)
- Logging levels and format
- Graceful degradation strategy

### 10. Testing Strategy
- Test locally with: claude --plugin-dir ./[plugin-name]
- Load multiple plugins: claude --plugin-dir ./plugin-one --plugin-dir ./plugin-two
- Debug with: claude --debug
- Unit tests for scripts and core logic
- Verify: commands appear in /help, agents in /agents, hooks fire on events

### 11. Versioning & Distribution
- Semantic versioning in plugin.json (bump on every change or cached versions won't update)
- Installation scopes: user (default), project (shared via git), local (gitignored)
- Marketplace packaging for claude plugin install
- CHANGELOG.md for version history

### 12. Build Order
- Step-by-step implementation sequence
- Which components to build and test first
- Milestone checkpoints to verify progress
- Common pitfalls to avoid:
  - Don't put components inside .claude-plugin/
  - Don't use absolute paths
  - Don't forget chmod +x on hook scripts
  - Don't reference files outside the plugin directory

Build this as a production-ready Claude Code plugin I can start using immediately. Prioritize working components over documentation — I want to ship this.
```

---

## Usage Notes

- If the user has not answered all qualifying questions, still include the unanswered questions as placeholders with "[Not specified — use your best judgment]"
- The architecture type should inform which sections are most relevant (e.g., a CLI tool may not need MCP servers, a Claude Code plugin may not need a database)
- Always include the plugin manifest and directory structure sections — these are required for all plugins
- Always include the testing section with `claude --plugin-dir` instructions
- Keep the generated prompt under 1000 words to stay focused
