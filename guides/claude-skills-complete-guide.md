---
title: "Claude Skills - Complete Guide & Tutorial"
date: 2025-10-18
draft: false
summary: "A comprehensive guide to understanding and using Claude Skills - reusable instruction sets that teach Claude how to perform specific tasks consistently in your daily workflow."
tags: ["Claude", "AI", "Skills", "Tutorial", "Development"]
authors: ["Prompt Stack"]
---

# Claude Skills - Complete Guide & Tutorial

**Last Updated:** October 18, 2025
**Your Reference Guide** for understanding and using Claude Skills in daily workflow

---

## 📖 Table of Contents

1. [What Are Skills?](#what-are-skills)
2. [Where Skills Live (Critical!)](#where-skills-live)
3. [How Skills Work Behind The Scenes](#how-skills-work)
4. [Community Resources & Tools](#community-resources--tools)
5. [Quick Start: Installing Existing Skills](#quick-start-installing-existing-skills)
6. [Creating Your First Skill](#creating-your-first-skill)
7. [Real-World Examples](#real-world-examples)
8. [Daily Workflow Usage](#daily-workflow-usage)
9. [Best Practices](#best-practices)
10. [Troubleshooting](#troubleshooting)

---

## What Are Skills?

**Skills are reusable instruction sets** that teach Claude how to perform specific tasks consistently. They're like hiring a specialist who already knows your company's way of doing things.

### The Problem They Solve

**Before Skills:**
```
You: "Add a new API endpoint"
Claude: "Sure! What framework are you using?"
You: "FastAPI with async"
Claude: "Got it. What about authentication?"
You: "Use our Clerk JWT pattern"
Claude: "And rate limiting?"
You: "10 requests per minute with FastAPILimiter"
... (repeat this EVERY time)
```

**With Skills:**
```
You: "Add a new API endpoint"
Claude: [Loads API Patterns Skill automatically]
        "Creating FastAPI endpoint with Clerk auth,
        rate limiting, and our standard error handling..."
```

### Key Benefits

- ✅ **Consistency** - Same workflow every time
- ✅ **Speed** - No re-explaining your patterns
- ✅ **Token Efficiency** - Only loads when relevant
- ✅ **Portability** - Works in Claude app, Claude Code, and API
- ✅ **Team Sharing** - Commit `.claude/skills/` to Git

---

## Where Skills Live (Critical!)

This is the **most important** thing to understand:

### Option 1: Global/Personal Skills
**Location:** `~/.claude/skills/`
**Full Path:** `/Users/hoff/.claude/skills/`

```bash
~/.claude/skills/
├── code-review-checklist/
│   └── SKILL.md
├── git-commit-style/
│   └── SKILL.md
└── python-best-practices/
    └── SKILL.md
```

**When to use:**
- ✅ Skills you use across ALL projects
- ✅ Personal coding standards
- ✅ General workflows (Git, documentation, testing)
- ✅ Language-specific patterns you always follow

### Option 2: Project-Specific Skills
**Location:** `.claude/skills/` (in your project root)
**Example:** `/Users/hoff/Desktop/My Drive/tools/data-processing/content-engine/.claude/skills/`

```bash
content-engine/
├── .claude/
│   └── skills/
│       ├── content-extraction-workflow/
│       │   └── SKILL.md
│       ├── api-endpoint-patterns/
│       │   └── SKILL.md
│       └── database-migrations/
│           └── SKILL.md
├── backend/
├── frontend/
└── docs/
```

**When to use:**
- ✅ Project-specific architecture patterns
- ✅ Domain knowledge for this codebase
- ✅ Team conventions (commit to Git so team uses same patterns)
- ✅ Project-specific workflows

### ⚠️ Important: Not Your Documentation Folder!

**DON'T put Skills here:**
```bash
❌ /Users/hoff/Desktop/My Drive/content/claude-skills/
   (This is for YOUR reference docs, not actual Skills)
```

**DO put Skills here:**
```bash
✅ ~/.claude/skills/                    (Global - all projects)
✅ /path/to/project/.claude/skills/     (Project-specific)
```

**BUT you can put guides/tutorials here:**
```bash
✅ /Users/hoff/Desktop/My Drive/content/topics/claude-skills-complete-guide.md
   (This guide you're reading now! For YOUR reference)
```

---

## How Skills Work Behind The Scenes

### The Magic: Progressive Loading

1. **Startup (Cheap)**
   ```
   Claude Code starts → Scans ~/.claude/skills/ and .claude/skills/
   → Reads ONLY the YAML metadata (name + description)
   → Loads ~20-50 tokens per Skill into memory
   → Total cost: Few hundred tokens for all your Skills
   ```

2. **User Request**
   ```
   You: "Add a YouTube extractor"
   Claude: Checks metadata of all Skills
   → "Content Extraction Workflow" description matches!
   → Loads full SKILL.md (2000+ tokens)
   → Uses instructions to complete task
   ```

3. **Irrelevant Skills Stay Unloaded**
   ```
   You: "Fix this CSS bug"
   Claude: Checks metadata
   → "Content Extraction Workflow" NOT relevant
   → Stays unloaded (saves tokens)
   → "Frontend Styling Standards" might load instead
   ```

### Token Comparison

| Approach | Tokens Used | Cost Impact |
|----------|-------------|-------------|
| **Re-explaining every time** | 500-2000 per request | High |
| **Skills (metadata only)** | ~30 per Skill | Minimal |
| **Skills (when loaded)** | ~2000 (but only once) | Efficient |
| **MCP (always loaded)** | 20,000-30,000+ | Expensive |

---

## Community Resources & Tools

The Skills ecosystem is growing rapidly! Here are the tools and resources that make creating and using Skills much easier.

### 🔥 Skill-Creator (The Meta Skill)

**What it is:** A Skill that creates Skills for you (yes, really!)

Anthropic built a Skill that writes SKILL.md files based on your plain English description. This is the **easiest way** to create custom Skills.

**How to use:**
1. Install the skill-creator from Anthropic's repo (see Quick Start below)
2. Tell Claude: *"Create a Skill for [describe your workflow]"*
3. Claude asks clarifying questions
4. It generates the complete SKILL.md file
5. You review and start using it

**Demo:** https://youtube.com/watch?v=kS1MJFZWMq4 (47 seconds)

**Why it's game-changing:**
- No manual SKILL.md writing
- Interactive guidance ensures you cover everything
- Follows Anthropic's best practices automatically
- Perfect for non-technical users

### 🤖 Skill Seekers - Auto-Generate from Documentation

**GitHub:** https://github.com/yusufkaraaslan/Skill_Seekers

**What it is:** An automated tool that turns ANY documentation site into a Claude Skill

**How it works:**
```bash
# Install
git clone https://github.com/yusufkaraaslan/Skill_Seekers
cd Skill_Seekers

# Generate a Skill from docs (takes ~25 minutes)
python skill_seekers.py --url https://fastapi.tiangolo.com

# Or use presets
python skill_seekers.py --preset fastapi
python skill_seekers.py --preset react
python skill_seekers.py --preset django
```

**Available presets:**
- FastAPI (perfect for your Content Engine backend!)
- React
- Vue
- Django
- Godot
- Next.js
- And more...

**Why this is huge:**
Instead of manually writing Skills for frameworks/libraries, just point Skill Seekers at the official docs and get a production-ready Skill in 25 minutes.

**Real-world results:**
- Community reports it works well for major frameworks
- The generated Skill "knows" framework details better than base Claude
- Saves hours of manual Skill writing

**Use case for you:**
```bash
# Generate Skills for your Content Engine stack:
skill_seekers.py --preset fastapi        # Backend patterns
skill_seekers.py --preset nextjs         # Frontend patterns
skill_seekers.py --url https://clerk.com/docs  # Clerk auth
skill_seekers.py --url https://alembic.sqlalchemy.org  # Migrations
```

### 📚 Community Collections - Ready-Made Skills

Don't build from scratch! Browse these curated collections of Skills created by the community:

#### BehiSecc's Awesome Claude Skills
**GitHub:** https://github.com/BehiSecc/awesome-claude-skills

**Includes:**
- CSV analyzers
- Research assistants
- YouTube transcript fetchers
- EPUB parsers
- Git automation workflows
- Data visualization Skills
- And 20+ more...

**Best for:** General-purpose Skills across different domains

#### travisvn's Awesome Claude Skills
**GitHub:** https://github.com/travisvn/awesome-claude-skills

**Includes:**
- Enterprise workflow automation
- Business reporting templates
- Project management Skills
- Documentation generators
- Code analysis tools

**Best for:** Professional/enterprise workflows

**How to use these:**
```bash
# Clone the repo
git clone https://github.com/BehiSecc/awesome-claude-skills

# Browse available Skills
cd awesome-claude-skills
ls -la skills/

# Install one you like
cp -r skills/csv-analyzer ~/.claude/skills/
# Now you can use it in any project!
```

### 🎨 Official Anthropic Skills Pack

**GitHub:** https://github.com/anthropics/skills

Anthropic released **15 official Skills** covering document creation, design, and development workflows.

#### Document & Office Skills
- **docx** - Create real Word documents (not markdown-as-Word)
  - Proper formatting, headers, tables
  - Styles and sections

- **pptx** - Professional PowerPoint presentations
  - Slide layouts
  - Charts and graphs
  - Speaker notes

- **xlsx** - Excel spreadsheets with formulas
  - Complex formulas
  - Multiple sheets
  - Data validation

- **pdf** - PDF manipulation
  - Form filling
  - Text extraction
  - Conversion

#### Creative & Design Skills
- **canvas-design** - Visual layouts as PNG/PDF
  - Typography
  - Layout composition
  - Export to image formats

- **brand-guidelines** - Consistent branding
  - Color schemes
  - Font families
  - Logo usage
  - Tone of voice

- **algorithmic-art** - Generative art with p5.js
  - Creative coding
  - Interactive visualizations
  - Export to canvas

- **slack-gif-creator** - GIFs optimized for Slack
  - Meets Slack's file constraints
  - Proper dimensions
  - File size limits

#### Development & Workflow Skills
- **skill-creator** - Creates Skills from descriptions
- **mcp-server-creator** - Build MCP servers
- **web-testing** - Automated web testing
- **internal-comms** - Team communication templates

**How to install:**
```bash
# Clone the official repo
git clone https://github.com/anthropics/skills anthropic-skills

# Install specific Skills you want
cd anthropic-skills
cp -r document-skills/docx ~/.claude/skills/
cp -r document-skills/pptx ~/.claude/skills/
cp -r skill-creator ~/.claude/skills/
```

**Study the source:**
The `document-skills/` folder shows how Anthropic builds complex Skills - great learning resource!

### 🧠 Expert Analysis: Simon Willison's Take

**Article:** https://simonwillison.net/2025/Oct/16/claude-skills/

Simon Willison (who reverse-engineered Skills before the official announcement) wrote an excellent technical deep-dive.

**Key insights:**
1. **Skills may be more important than MCP in the long run**
   - Simpler to create (Markdown + YAML vs. full protocol)
   - More token-efficient (progressive loading vs. always-on)
   - Easier to share (just files vs. server setup)

2. **Progressive disclosure is the killer feature**
   - Each Skill costs ~30 tokens until needed
   - MCP can cost 20,000-30,000+ tokens upfront
   - Skills scale better as you add more

3. **Skills fit the LLM paradigm better**
   - "Throw text at the model, let it figure it out"
   - Natural for AI systems
   - Lower barrier to entry

**His prediction:** Skills will become the primary way people customize Claude for specific domains.

### 🎬 Official Demo Videos

**Skills Overview & Chaining:**
https://youtube.com/watch?v=IoqpBKrNaZI

Shows Skills working together automatically:
- PowerPoint Skill → Brand Guidelines Skill → Poster Design Skill
- All in one conversation
- Claude switches between them seamlessly

**Skill-Creator Demo:**
https://youtube.com/watch?v=kS1MJFZWMq4

47-second demo of creating a Skill just by describing it.

---

## Quick Start: Installing Existing Skills

Want to start using Skills **right now** without creating your own? Here's how to get up and running in minutes.

### Option 1: Install Official Anthropic Skills

**Most popular picks for developers:**

```bash
# Clone the official Skills repo
cd ~/Downloads
git clone https://github.com/anthropics/skills anthropic-skills
cd anthropic-skills

# Install the skill-creator (meta-skill for creating Skills)
cp -r skill-creator ~/.claude/skills/

# Install document creation Skills
cp -r document-skills/docx ~/.claude/skills/
cp -r document-skills/pptx ~/.claude/skills/
cp -r document-skills/xlsx ~/.claude/skills/

# Install development Skills
cp -r mcp-server-creator ~/.claude/skills/
```

**Test it:**
```
Ask Claude: "Create a Word document with project status report"
Claude will use the docx Skill automatically!
```

### Option 2: Install Community Skills

**For your Content Engine project:**

```bash
# Clone community collection
cd ~/Downloads
git clone https://github.com/BehiSecc/awesome-claude-skills

# Browse what's available
cd awesome-claude-skills
ls -la skills/

# Install useful ones for data/content work
cp -r skills/csv-analyzer ~/.claude/skills/
cp -r skills/youtube-transcript ~/.claude/skills/
cp -r skills/research-assistant ~/.claude/skills/
```

### Option 3: Auto-Generate from Your Stack's Docs

**Generate Skills for your actual tech stack:**

```bash
# Install Skill Seekers
git clone https://github.com/yusufkaraaslan/Skill_Seekers
cd Skill_Seekers

# Generate FastAPI Skill (your backend framework)
python skill_seekers.py --preset fastapi
# Wait ~25 minutes
# Skill is saved to output directory

# Copy to your Skills folder
cp -r output/fastapi-skill ~/.claude/skills/

# Repeat for other frameworks you use:
python skill_seekers.py --preset nextjs     # Frontend
python skill_seekers.py --preset react      # If using React components
```

### Option 4: Use Skill-Creator to Make Custom Skills

**For Content Engine-specific workflows:**

```bash
# First, install skill-creator
git clone https://github.com/anthropics/skills
cp -r skills/skill-creator ~/.claude/skills/

# Then in Claude Code, tell Claude:
```

```
"Create a Skill for my API endpoint pattern. We use:
- FastAPI with async/await
- Clerk JWT authentication
- FastAPILimiter (10 req/min)
- Standardized error responses
- PostgreSQL with SQLAlchemy"
```

Claude will:
1. Ask clarifying questions
2. Generate a complete SKILL.md
3. Save it to your project's `.claude/skills/` folder
4. ✅ Ready to use!

### Installation Checklist

**Recommended starter pack:**

Global Skills (install to `~/.claude/skills/`):
- ✅ skill-creator (for making more Skills easily)
- ✅ docx (for documentation)
- ✅ Your framework's Skill (FastAPI, React, etc.)
- ✅ Git workflow Skill (from community)

Project Skills (install to `content-engine/.claude/skills/`):
- ✅ content-extraction-workflow (already created!)
- ✅ api-endpoint-patterns (create with skill-creator)
- ✅ database-migrations (create with skill-creator)

**After installation:**
```bash
# Verify what Skills are available
ls -la ~/.claude/skills/
ls -la .claude/skills/

# Test in Claude Code
# Just ask Claude to do something the Skill covers!
```

---

## Creating Your First Skill

You have **four ways** to create Skills, from easiest to most manual:

### Method 1: Use Skill-Creator (Recommended!)

**Prerequisites:** Install skill-creator first (see Quick Start section above)

Then just tell Claude what you want:

```
"Create a Skill for my API endpoint pattern. We use:
- FastAPI with async/await
- Clerk JWT authentication
- FastAPILimiter for rate limiting (10 req/min)
- Standardized error responses
- PostgreSQL with SQLAlchemy ORM"
```

Claude (via skill-creator Skill) will:
1. Ask clarifying questions about your workflow
2. Generate the complete SKILL.md file with proper structure
3. Save it to `.claude/skills/` or `~/.claude/skills/`
4. ✅ Ready to use immediately!

**Why this is best:**
- No manual file editing
- Interactive process ensures completeness
- Follows Anthropic's best practices
- Works for non-technical users

### Method 2: Auto-Generate from Documentation (For Frameworks)

**Use Skill Seekers** when you want a Skill for an existing framework/library:

```bash
# Install Skill Seekers
git clone https://github.com/yusufkaraaslan/Skill_Seekers
cd Skill_Seekers

# Generate from preset
python skill_seekers.py --preset fastapi

# Or from any docs URL
python skill_seekers.py --url https://your-framework-docs.com

# Wait ~25 minutes, then install
cp -r output/generated-skill ~/.claude/skills/
```

**Best for:**
- Framework-specific Skills (React, Django, FastAPI, etc.)
- Library documentation (SQLAlchemy, Alembic, etc.)
- Technical documentation with clear structure

### Method 3: Clone and Customize Community Skills

Browse the awesome-claude-skills repos and fork existing Skills:

```bash
git clone https://github.com/BehiSecc/awesome-claude-skills
cd awesome-claude-skills/skills/

# Find one similar to what you need
cat csv-analyzer/SKILL.md

# Copy and modify
cp -r csv-analyzer ~/.claude/skills/my-data-analyzer
nano ~/.claude/skills/my-data-analyzer/SKILL.md
# Edit to match your needs
```

**Best for:**
- When you find a Skill that's 80% what you need
- Learning Skill structure by example
- Quick customization

### Method 4: Manual Creation (Full Control)

If you want complete control over the Skill structure:

**Step 1: Create the directory**
```bash
mkdir -p ~/.claude/skills/my-api-pattern
cd ~/.claude/skills/my-api-pattern
```

**Step 2: Create SKILL.md**
```markdown
---
name: "API Endpoint Pattern"
description: "Create FastAPI endpoints with Clerk auth, rate limiting, and error handling following our standard architecture"
version: 1.0.0
---

## Overview
This Skill defines our standard pattern for creating API endpoints.

## Required Imports
```python
from fastapi import APIRouter, HTTPException, Depends
from fastapi_limiter.depends import RateLimiter
from app.core.clerk import get_current_user_from_clerk
from app.models.user import User
```

## Standard Endpoint Template
```python
router = APIRouter()

@router.post("/resource", dependencies=[Depends(RateLimiter(times=10, seconds=60))])
async def create_resource(
    data: ResourceRequest,
    current_user: User = Depends(get_current_user_from_clerk)
):
    try:
        # Implementation
        return {"status": "success", "data": result}
    except ValueError as e:
        raise HTTPException(status_code=400, detail=str(e))
    except Exception as e:
        raise HTTPException(status_code=500, detail=f"Operation failed: {str(e)}")
```

## Error Handling Rules
- 400: Bad request / validation errors
- 401: Authentication required
- 403: Permission denied
- 404: Resource not found
- 429: Rate limit exceeded
- 500: Internal server error

## Always Include
1. Rate limiting via RateLimiter dependency
2. Clerk authentication for protected endpoints
3. Standardized error responses
4. Type hints on all parameters
5. Docstring with endpoint description
```

**Step 3: Test it**
```bash
# In Claude Code, ask:
"Add a new endpoint for creating posts"

# Claude will automatically load your Skill and follow the pattern!
```

---

## Real-World Examples

### Example 1: Content Engine Extractor Pattern

**File:** `/Users/hoff/Desktop/My Drive/tools/data-processing/content-engine/.claude/skills/content-extraction-workflow/SKILL.md`

**What it does:**
- Teaches Claude the BaseExtractor pattern
- Defines fallback strategy (API → Library → CLI → Scraping)
- Specifies output format
- Lists file locations
- Sets code style guidelines

**Usage:**
```
You: "Add a Reddit extractor"
Claude: [Loads Skill] → Creates extractor following BaseExtractor
                      → Implements fallback strategy
                      → Uses Clerk auth
                      → Formats output correctly
```

### Example 2: Database Migration Pattern

**Create this Skill:**
```bash
mkdir -p .claude/skills/database-migrations
```

**SKILL.md:**
```markdown
---
name: "Database Migration Pattern"
description: "Create Alembic migrations following our safety-first approach with rollback procedures"
version: 1.0.0
---

## Migration Safety Rules

1. **Always check existing tables** before creating/dropping
   ```python
   conn = op.get_bind()
   inspector = inspect(conn)

   if 'table_name' not in inspector.get_table_names():
       # Safe to create
   ```

2. **Never auto-generate drop commands** - Review all drops manually

3. **Make migrations reversible** - Always implement downgrade()

4. **Test locally** before deploying to production

## File Location
`backend/alembic/versions/`

## Naming Convention
`{revision}_descriptive_name.py`

Example: `6cb13d089f5e_recreate_captures_table_after_accidental_drop.py`
```

### Example 3: Git Commit Style (Global Skill)

**File:** `~/.claude/skills/git-commit-style/SKILL.md`

```markdown
---
name: "Git Commit Style"
description: "Format Git commit messages following Conventional Commits with my preferred structure"
version: 1.0.0
---

## Commit Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

## Types
- feat: New feature
- fix: Bug fix
- docs: Documentation only
- refactor: Code refactoring
- test: Adding tests
- chore: Maintenance

## Examples

```
feat(auth): Migrate LLM endpoints to Clerk authentication

- Updated /api/llm/generate endpoint
- Updated /api/llm/process-content endpoint
- Removed verify_api_key dependency
- Added comprehensive deprecation warnings

Refs: #123
```

## Rules
- Subject line: max 72 characters
- Body: wrap at 80 characters
- Always include "why" in body, not just "what"
```

---

## Daily Workflow Usage

### Scenario 1: Starting a New Project

**Setup Project Skills:**
```bash
cd /path/to/new-project
mkdir -p .claude/skills

# Create skills for:
# - Architecture patterns
# - Testing standards
# - Code review checklist
# - Deployment workflow
```

**Usage:**
Now every time you work on this project, Claude automatically follows your patterns without re-explaining!

### Scenario 2: Working on Content Engine

**Morning workflow:**
```bash
cd ~/Desktop/My\ Drive/tools/data-processing/content-engine
code .  # Open in VS Code with Claude Code

# Skills automatically available:
# - content-extraction-workflow ✅
# - api-endpoint-patterns (if you create it)
# - database-migrations (if you create it)
```

**During development:**
```
You: "Add Instagram extractor"
Claude: [Auto-loads content-extraction-workflow]
        → Follows BaseExtractor pattern
        → Implements multi-tier fallback
        → Uses standardized output format
        → Adds Clerk auth
        ✅ Consistent with existing extractors!

You: "Create migration to add user preferences"
Claude: [Auto-loads database-migrations skill]
        → Checks if table exists first
        → Makes migration reversible
        → Follows naming convention
        ✅ Safe migration created!
```

### Scenario 3: Working Across Multiple Projects

**Global Skills Help Everywhere:**
```bash
# Skills in ~/.claude/skills/ are available in ALL projects:
~/.claude/skills/
├── code-review/        → Used in every project
├── git-commits/        → Used in every project
├── python-typing/      → Used in Python projects
└── api-security/       → Used in web projects

# Project skills are project-specific:
content-engine/.claude/skills/content-extraction/  → Only here
my-blog/.claude/skills/blog-post-format/           → Only here
startup-mvp/.claude/skills/mvp-shortcuts/          → Only here
```

---

## Best Practices

### ✅ DO

1. **Keep Skills Focused**
   - ✅ Separate Skill for each workflow
   - ❌ One giant Skill for everything

2. **Write Clear Descriptions**
   ```yaml
   # Good
   description: "Create FastAPI endpoints with Clerk JWT auth and rate limiting"

   # Bad
   description: "API stuff"
   ```

3. **Include Examples**
   - Show Claude what good output looks like
   - Include code snippets
   - Reference existing files

4. **Version Your Skills**
   ```yaml
   version: 1.0.0  # Increment when you update
   ```

5. **Commit Project Skills to Git**
   ```bash
   git add .claude/skills/
   git commit -m "chore: Add content extraction workflow Skill"
   ```
   Now your whole team follows the same patterns!

### ❌ DON'T

1. **Don't Make Skills Too Generic**
   ```yaml
   # Too generic - won't trigger correctly
   description: "Help with coding"

   # Better - specific trigger conditions
   description: "Create Python FastAPI endpoints with async/await patterns"
   ```

2. **Don't Put Secrets in Skills**
   ```markdown
   ❌ API_KEY=sk-1234567890
   ✅ API keys are in .env file
   ```

3. **Don't Duplicate Global and Project Skills**
   - If it applies everywhere → Global (`~/.claude/skills/`)
   - If it's project-specific → Project (`.claude/skills/`)

4. **Don't Overwhelm with Too Many Skills**
   - Start with 2-3 most important workflows
   - Add more as needed

---

## Troubleshooting

### "Claude isn't using my Skill"

**Check these:**

1. **File location correct?**
   ```bash
   # Verify file exists:
   ls ~/.claude/skills/my-skill/SKILL.md
   # OR
   ls .claude/skills/my-skill/SKILL.md
   ```

2. **Valid YAML frontmatter?**
   ```markdown
   ---
   name: "Skill Name"
   description: "When to use this"
   ---
   ✅ Three dashes, valid YAML
   ```

3. **Description specific enough?**
   ```yaml
   # Too vague
   description: "Coding help"

   # Better
   description: "Create React components using TypeScript with our standard props pattern"
   ```

4. **Is request relevant to Skill?**
   ```
   Request: "Add API endpoint"
   Skill description: "Frontend React patterns"
   → Won't match! Make description match use cases
   ```

### "How do I see what Skills are loaded?"

Ask Claude:
```
"What Skills are available in this project?"
```

### "Can I disable a Skill temporarily?"

Yes! Rename the folder:
```bash
mv .claude/skills/my-skill .claude/skills/my-skill.disabled
```

Or remove it:
```bash
rm -rf .claude/skills/my-skill
```

---

## Quick Reference Card

### File Locations Cheat Sheet

```
Global Skills (All Projects):
~/.claude/skills/my-skill/SKILL.md

Project Skills (This Project Only):
.claude/skills/my-skill/SKILL.md

Documentation (Your Reference):
/Users/hoff/Desktop/My Drive/content/topics/
```

### SKILL.md Template

```markdown
---
name: "Skill Name Here"
description: "One-line description of when to use this (max 1024 chars)"
version: 1.0.0
---

## Overview
What this Skill does and when to use it.

## Instructions
Step-by-step guidance for Claude.

## Examples
Show concrete examples.

## Reference Files
Point to example implementations.
```

### Common Commands

```bash
# Create new Skill
mkdir -p .claude/skills/my-skill
nano .claude/skills/my-skill/SKILL.md

# List project Skills
ls -la .claude/skills/

# List global Skills
ls -la ~/.claude/skills/

# Test Skill
# Just ask Claude to do something the Skill covers!
```

---

## Next Steps

### For Your Content Engine:

**Already Created:**
✅ Content Extraction Workflow Skill

**Recommended Next Skills:**
1. **API Endpoint Patterns** - FastAPI + Clerk + Rate Limiting
2. **Database Migration Safety** - Alembic best practices
3. **Frontend Component Pattern** - React/Next.js conventions
4. **Testing Standards** - pytest patterns for extractors

### Create Your First Global Skill:

```bash
mkdir -p ~/.claude/skills/code-review
```

Add your personal code review checklist that applies to every project!

---

## Resources

### Official Anthropic Resources
- **Claude Code Skills Docs:** https://docs.claude.com/en/docs/claude-code/skills
- **API Skills Guide:** https://docs.claude.com/en/api/skills-guide
- **Official Skills Repository:** https://github.com/anthropics/skills
- **Engineering Deep-Dive:** https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
- **Announcement Blog:** https://www.anthropic.com/news/skills

### Community Tools
- **Skill Seekers (Auto-Generator):** https://github.com/yusufkaraaslan/Skill_Seekers
  - Turn documentation into Skills automatically
  - Presets for FastAPI, React, Django, Next.js, etc.

### Community Collections
- **BehiSecc's Awesome Claude Skills:** https://github.com/BehiSecc/awesome-claude-skills
  - CSV analyzers, research assistants, YouTube tools, Git automation

- **travisvn's Awesome Claude Skills:** https://github.com/travisvn/awesome-claude-skills
  - Enterprise workflows, business reporting, project management

### Expert Analysis
- **Simon Willison's Deep-Dive:** https://simonwillison.net/2025/Oct/16/claude-skills/
  - Technical analysis
  - Skills vs MCP comparison
  - Progressive disclosure explanation

### Demo Videos
- **Skills Overview & Chaining:** https://youtube.com/watch?v=IoqpBKrNaZI
- **Skill-Creator Demo:** https://youtube.com/watch?v=kS1MJFZWMq4 (47 seconds)

### Your Local Skills
- **Content Engine Extractor Workflow:** `.claude/skills/content-extraction-workflow/`
- **Global Skills Directory:** `~/.claude/skills/`
- **Project Skills Directory:** `.claude/skills/`

### Quick Start Commands
```bash
# Install official Skills
git clone https://github.com/anthropics/skills
cp -r skills/skill-creator ~/.claude/skills/

# Install community Skills
git clone https://github.com/BehiSecc/awesome-claude-skills

# Generate from docs
git clone https://github.com/yusufkaraaslan/Skill_Seekers
cd Skill_Seekers && python skill_seekers.py --preset fastapi

# List your installed Skills
ls -la ~/.claude/skills/
ls -la .claude/skills/
```

---

**Remember:** Skills are about teaching Claude **your way of working** once, then having it remember across all your conversations. It's like onboarding a new team member who never forgets the company handbook!

**Get Started Today:**
1. Install skill-creator: `git clone https://github.com/anthropics/skills && cp -r skills/skill-creator ~/.claude/skills/`
2. Tell Claude: *"Create a Skill for my [workflow]"*
3. Watch as Claude follows your patterns automatically from now on!

The Skills ecosystem is growing daily - check the community repos regularly for new Skills that might save you time!
