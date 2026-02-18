# Build Prompt Template

When the user clicks "Copy Blueprint Prompt" on a plugin card, generate a prompt following this template. Replace all bracketed placeholders with actual values from the plugin data and the user's answers.

---

## Template

```
Design and build me a complete plugin called "[PLUGIN NAME]".

## Overview
[PLUGIN DESCRIPTION]

## Architecture Type
[ARCHITECTURE TYPE] (e.g., API Integration, CLI Tool, Full-Stack Web App, etc.)

## My Requirements
[For each answered question, include:]
- [Question text]: [User's answer]

## What I Need You to Deliver

### 1. Architecture Overview
- System design diagram (describe components and their interactions in text/ASCII)
- Data flow between components
- External service dependencies
- Key architectural decisions and trade-offs

### 2. Tech Stack
- Language and runtime with version
- Framework(s) with justification for each choice
- Database (if applicable) with schema rationale
- Key libraries and dependencies
- Why this stack over alternatives for this use case

### 3. Project Structure
- Complete directory tree
- Purpose of each top-level directory
- Key files and their responsibilities
- Configuration file locations

### 4. Database Schema (if applicable)
- Table/collection definitions with fields, types, and constraints
- Relationships and indexes
- Migration strategy
- Seed data (if helpful)

### 5. API / Interface Design
- All endpoints or commands with request/response shapes
- Authentication and authorization scheme
- Rate limiting and validation rules
- Error response format

### 6. Core Implementation
- Implement the main modules with full, working code
- Include inline comments explaining non-obvious logic
- Handle edge cases and errors properly
- Follow the language/framework's idiomatic patterns

### 7. Authentication & Authorization (if applicable)
- Auth flow (OAuth, API keys, JWT, etc.)
- Permission model
- Session/token management
- Security considerations

### 8. Error Handling & Logging
- Error taxonomy (expected vs unexpected)
- Logging levels and format
- Monitoring hooks or health checks
- Graceful degradation strategy

### 9. Testing Strategy
- Unit tests for core business logic
- Integration tests for API/external services
- Test fixtures and mocks
- How to run the test suite

### 10. Deployment & CI/CD
- Dockerfile or deployment configuration
- CI/CD pipeline definition (GitHub Actions, etc.)
- Environment variable documentation
- Infrastructure requirements

### 11. Configuration
- All environment variables with descriptions and defaults
- Configuration file format and location
- Secrets management approach
- Development vs production config differences

### 12. Build Order
- Step-by-step implementation sequence
- Which components to build and test first
- Dependencies between components
- Milestone checkpoints to verify progress

Build this as production-ready code I can start using immediately. Prioritize working software over documentation — I want to ship this.
```

---

## Usage Notes

- If the user has not answered all qualifying questions, still include the unanswered questions as placeholders with "[Not specified — use your best judgment]"
- The architecture type should inform which sections are most relevant (e.g., a CLI tool doesn't need a database schema section, a browser extension doesn't need deployment/CI/CD in the same way)
- Keep the generated prompt under 800 words to stay focused
