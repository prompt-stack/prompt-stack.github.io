---
layout: page
title: Projects
permalink: /projects/
---

# Projects

Production-ready applications built with AI-assisted development.

---

## [Content Engine](https://github.com/prompt-stack/content-engine)

**Full-stack AI content processing platform**

Extract, process, and synthesize information from social platforms. Built with FastAPI + Next.js, PostgreSQL, Clerk auth, and multi-provider LLM integration.

- **Live Demo**: [content-engine-frontend-green.vercel.app](https://content-engine-frontend-green.vercel.app)
- **Tech Stack**: FastAPI, Next.js 15, PostgreSQL, Redis, Clerk
- **Deployment**: Railway + Vercel

[View Repository →](https://github.com/prompt-stack/content-engine)

---

## [Content Stack](https://github.com/prompt-stack/content-stack)

**AI-powered content management platform**

Media processor with analyze, generate, and transform capabilities. Component-driven architecture with strict design system.

- **Tech Stack**: React 19, TypeScript, Vite, Express
- **Features**: Media processing, terminal orchestration
- **Architecture**: BEM methodology with CSS auditing

[View Repository →](https://github.com/prompt-stack/content-stack)

---

## [Prompt Stack Lite](https://github.com/prompt-stack/prompt-stack-lite)

**AI Development Studio**

The fastest way to build and ship AI products. Includes authentication, payments, AI integration, and vector search out of the box.

- **Tech Stack**: Next.js 15 + FastAPI
- **Features**: Demo mode, Supabase auth, payments
- **AI**: OpenAI, Anthropic, Gemini, DeepSeek

[View Repository →](https://github.com/prompt-stack/prompt-stack-lite)

---

{% for project in site.projects %}
## [{{ project.title }}]({{ project.url }})

{{ project.summary }}

[Read more →]({{ project.url }})

---
{% endfor %}
