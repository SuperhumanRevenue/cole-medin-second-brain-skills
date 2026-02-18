# Plugin Archetypes

Use these archetypes to classify plugin opportunities and tailor qualifying questions.

## Archetype Reference

### API Integration
**What it is:** Connects two or more services via their APIs, syncing data or triggering actions.
**Typical stack:** Node.js/Python, REST/GraphQL clients, webhook handlers, queue (Redis/SQS)
**Best for:** Bridging tools that don't natively talk to each other
**Key questions:** Which APIs? Authentication method? Sync frequency? Error retry policy?
**Examples:** Stripe-to-Notion invoice sync, GitHub-to-Slack deployment notifier, CRM-to-email enrichment

### Webhook Pipeline
**What it is:** Event-driven pipeline that reacts to incoming webhooks, transforms data, and routes it.
**Typical stack:** Serverless functions (AWS Lambda, Cloudflare Workers), message queues, transformation logic
**Best for:** Real-time event processing across systems
**Key questions:** Event sources? Payload format? Transformation rules? Delivery targets?
**Examples:** Payment event processor, form submission router, CI/CD status aggregator

### CLI Tool
**What it is:** Command-line utility for developer or ops workflows.
**Typical stack:** Python (Click/Typer), Rust (Clap), Go (Cobra), Node (Commander)
**Best for:** Automating repetitive terminal tasks, scripting complex operations
**Key questions:** Primary commands? Input sources? Output format? OS targets?
**Examples:** Database migration runner, log analyzer, project scaffolder, deployment helper

### Full-Stack Web App
**What it is:** Complete web application with frontend, backend, and database.
**Typical stack:** React/Next.js/SvelteKit + API layer + PostgreSQL/SQLite + auth
**Best for:** User-facing tools, dashboards, admin panels, SaaS products
**Key questions:** User count? Auth method? Core entities? Real-time needs? Hosting preference?
**Examples:** Client portal, analytics dashboard, project management tool, booking system

### Browser Extension
**What it is:** Chrome/Firefox extension that enhances or automates browser-based workflows.
**Typical stack:** Manifest V3, content scripts, service workers, popup UI (React/Svelte/vanilla)
**Best for:** Augmenting existing web apps, capturing data from pages, injecting functionality
**Key questions:** Target sites? Permissions needed? Background processing? Storage needs?
**Examples:** LinkedIn lead scraper, meeting note capturer, page annotator, price tracker

### Desktop App
**What it is:** Native or cross-platform desktop application.
**Typical stack:** Electron, Tauri (Rust + web), or native (Swift/C#)
**Best for:** System-level access, offline-first tools, menu bar utilities
**Key questions:** OS targets? System access needed? Offline requirements? Update mechanism?
**Examples:** Clipboard manager, screen recorder, file organizer, system monitor

### Mobile App
**What it is:** iOS/Android application, native or cross-platform.
**Typical stack:** React Native, Flutter, Swift/Kotlin
**Best for:** On-the-go access, push notifications, device sensor usage
**Key questions:** Platforms? Offline support? Push notifications? Device features?
**Examples:** Field data collector, expense tracker, team check-in app

### Slack/Discord Bot
**What it is:** Conversational bot integrated into a messaging platform.
**Typical stack:** Bolt (Slack SDK), Discord.js, serverless hosting
**Best for:** Team automations, status checks, interactive workflows in chat
**Key questions:** Commands needed? Interactive components? External data sources? Permissions?
**Examples:** Standup bot, incident commander, knowledge base searcher, approval workflow

### VS Code Extension
**What it is:** Extension for Visual Studio Code that enhances the development experience.
**Typical stack:** TypeScript, VS Code Extension API, Language Server Protocol
**Best for:** Developer tooling, code generation, linting, custom commands
**Key questions:** Activation events? UI contributions? Language support? External dependencies?
**Examples:** Custom snippet manager, API client generator, test runner, documentation helper

### Data Pipeline
**What it is:** ETL/ELT pipeline that extracts, transforms, and loads data on a schedule.
**Typical stack:** Python (pandas, dbt, Airflow), SQL, cloud storage, scheduler (cron, Airflow, Prefect)
**Best for:** Reporting, analytics, data warehouse feeding, periodic sync jobs
**Key questions:** Data sources? Volume? Frequency? Transformation complexity? Destination?
**Examples:** Daily sales report generator, multi-source analytics aggregator, data warehouse loader

### AI/LLM Plugin
**What it is:** Plugin that leverages AI models for intelligent processing or generation.
**Typical stack:** OpenAI/Anthropic API, vector database (Pinecone, ChromaDB), embedding pipeline
**Best for:** Content generation, classification, search, summarization, chatbots
**Key questions:** Model provider? Input type? Latency tolerance? Context/RAG needs? Cost budget?
**Examples:** Document summarizer, smart email responder, semantic search engine, content classifier

### Scheduled Automation
**What it is:** Time-triggered automation that runs on a schedule without user interaction.
**Typical stack:** Cron jobs, cloud scheduler, serverless functions, notification system
**Best for:** Periodic maintenance, report generation, monitoring, cleanup tasks
**Key questions:** Schedule frequency? Data sources? Output/notification method? Failure handling?
**Examples:** Weekly report emailer, stale PR notifier, database backup verifier, uptime checker

## Choosing the Right Archetype

| Signal in User's Workflow | Suggested Archetype |
|---------------------------|---------------------|
| "I copy data between X and Y" | API Integration |
| "When X happens I need to do Y" | Webhook Pipeline |
| "I run this command sequence often" | CLI Tool |
| "I need a dashboard for..." | Full-Stack Web App |
| "I do this manually on every webpage" | Browser Extension |
| "I need this on my desktop always" | Desktop App |
| "I need this on my phone" | Mobile App |
| "I wish I could do this from Slack" | Slack/Discord Bot |
| "I wish VS Code could..." | VS Code Extension |
| "I pull this report every week" | Data Pipeline |
| "I need AI to process..." | AI/LLM Plugin |
| "This should just happen automatically" | Scheduled Automation |
