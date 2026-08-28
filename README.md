# Agentic AI Lab

**Independent engineering sandbox for production-minded agentic AI patterns**

This repository is a build-in-public lab for exploring how multi-agent systems, tool use, permissions, data boundaries, and full-stack application architecture fit together in a realistic product environment.

The goal is not to publish employer or client code. Everything here is independent, synthetic, and designed from scratch to demonstrate transferable engineering skills.

## What this lab will demonstrate

- Multi-agent orchestration
- Tool / MCP-style integration patterns
- Role-based access control (RBAC)
- React / Next.js application architecture
- PostgreSQL + Prisma data modeling
- Authentication and session boundaries
- Human-in-the-loop workflows
- Testing and observability for AI-assisted features
- Production-minded failure handling

## Why this exists

A lot of AI portfolio work stops at “send a prompt, display a response.” That does not demonstrate the engineering challenges that matter in a real application.

This lab is intended to answer harder questions:

- What can each agent actually do?
- Which tools can it access?
- What happens when a tool fails?
- How are user permissions enforced independently of model behavior?
- How do we prevent an AI layer from bypassing application security?
- Where should deterministic code override probabilistic behavior?
- How do we inspect what happened after an agent takes multiple steps?

## Planned stack

- **Frontend:** Next.js, React, TypeScript, Tailwind CSS
- **AI:** Anthropic Claude API
- **Tooling:** MCP-compatible / explicit tool interfaces
- **Data:** PostgreSQL, Prisma
- **Testing:** Vitest, Playwright
- **Delivery:** GitHub Actions

## Initial scenario

The first implementation will use a **synthetic operations-training environment**. Users with different roles will work through guided tasks while AI agents can retrieve information, call permitted tools, and assist with workflow completion.

No FedEx, WillowTree, TELUS Digital, Virginia Lottery, or other employer/client source code, prompts, screenshots, schemas, or proprietary implementation details will be used.

## Architecture direction

```text
User
 |
 v
Next.js Application
 |
 +--> Authentication / RBAC
 |
 +--> Application services
 |       |
 |       +--> PostgreSQL / Prisma
 |
 +--> Agent orchestration
         |
         +--> Agent A
         +--> Agent B
         +--> Agent C
                 |
                 v
          Explicit tool layer
```

## Repository status

**Current status: architecture and implementation planning.**

This README intentionally distinguishes planned work from shipped work. As features are implemented, this section will be updated with working screenshots, architecture decisions, tests, and demo instructions.

See [`docs/architecture.md`](docs/architecture.md) for the initial design plan.

## What this portfolio project is meant to prove

This lab is less about a clever chatbot and more about showing the engineering surrounding AI systems: permissions, boundaries, data flow, failure modes, maintainability, and product behavior.

## About the builder

I’m Terin Pulley, a software engineer working across mobile, full-stack, and agentic AI systems. This project is an independent portfolio lab and is not affiliated with any employer or client.
