---
title:
date: 2025-10-18
type: landing

sections:
  - block: hero
    content:
      title: |
        Prompt Stack
        Engineering Knowledge Through Prompts
      text: |
        <br>

        **AI-powered tools for building, processing, and shipping software.**

        The Prompt Stack ecosystem provides production-ready applications for content processing, AI development, and knowledge synthesis. Built with modern full-stack architectures and deployed at scale.

  - block: markdown
    content:
      title: Products
      subtitle: Production-ready AI applications
      text: |
        ### [Content Engine](https://github.com/prompt-stack/content-engine)
        **Full-stack AI content processing platform**

        Extract, process, and synthesize information from social platforms (YouTube, Twitter, TikTok, Articles). Built with FastAPI + Next.js, PostgreSQL, Clerk auth, and multi-provider LLM integration (OpenAI, Anthropic, Gemini, DeepSeek).

        - **Backend:** FastAPI, PostgreSQL, Redis rate limiting, Alembic migrations
        - **Frontend:** Next.js 15, TypeScript, Tailwind CSS
        - **Deployment:** Railway + Vercel with auto-deployment
        - **Features:** Content vault, newsletter extraction, prompt management, JWT auth

        [View Repository →](https://github.com/prompt-stack/content-engine)

        ---

        ### [Content Stack](https://github.com/prompt-stack/content-stack)
        **AI-powered content management platform**

        Media processor with analyze, generate, and transform capabilities. Terminal agent orchestrator with multi-platform integration.

        - **Stack:** React, TypeScript, modern UI components
        - **Features:** Media processing, terminal orchestration, platform integrations
        - **Architecture:** Component-based design with modular services

        [View Repository →](https://github.com/prompt-stack/content-stack)

        ---

        ### [Prompt Stack Lite](https://github.com/prompt-stack/prompt-stack-lite)
        **AI Development Studio**

        The fastest way to build and ship AI products. Includes authentication, payments, AI integration, and vector search out of the box.

        - **Stack:** Next.js 15 App Router + FastAPI
        - **Features:** Demo mode, Supabase auth, Stripe/LemonSqueezy payments
        - **AI Providers:** OpenAI, Anthropic, Gemini, DeepSeek
        - **DX:** Docker Compose, hot reload, automatic migrations

        [View Repository →](https://github.com/prompt-stack/prompt-stack-lite)

    design:
      columns: '1'

  - block: markdown
    content:
      title: Technical Philosophy
      subtitle: From syntax to systems
      text: |
        **LLMs democratize access to programming languages.**

        AI tools like Claude Code collapse the syntax barrier - you can "make it run" without knowing why it runs. But production engineering still demands understanding: data contracts, state management, authentication, testing, deployment, cost optimization, and risk mitigation.

        This is the shift from **syntax to systems**. From **translation tax to infrastructure access**.

        The projects here demonstrate that shift - real code, working deployments, actionable patterns.

    design:
      columns: '1'
      background:
        color: '#f5f5f5'
      spacing:
        padding: ['40px', '0', '40px', '0']

  - block: collection
    content:
      title: Latest Guides
      subtitle: Technical deep-dives and tutorials
      text:
      count: 5
      filters:
        folders:
          - guides
      offset: 0
      order: desc
    design:
      view: card
      columns: '2'

  - block: markdown
    content:
      title: The Core Insight
      subtitle:
      text: |
        AI-assisted development isn't about replacing syntax with automation.

        It's about **prompting systems** to reveal their patterns, then **engineering solutions** with that understanding.

        As Pierre Bourdieu showed, **linguistic capital** - fluency in the languages that matter - converts to social and economic mobility. In a digitized society, those languages include Python, APIs, prompts, and systems thinking.

        **This site documents that exploration.**

    design:
      columns: '1'

  - block: markdown
    content:
      title: Open Source
      subtitle:
      text: |
        All projects are open source and available on GitHub.

        {{% cta cta_link="https://github.com/prompt-stack" cta_text="View Organization →" %}}
    design:
      columns: '1'
---
