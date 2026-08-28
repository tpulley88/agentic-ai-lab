# Agentic AI Lab — Architecture Plan

## Objective

Build a small but realistic agentic application where AI behavior is constrained by application permissions, explicit tools, and deterministic business rules.

The project should demonstrate that an agentic system is still a software system: authentication, authorization, data modeling, error handling, testing, and observability matter as much as the model call.

## Proposed system shape

```text
Browser
  |
  v
Next.js UI
  |
  v
Application API / server layer
  |
  +--> Authentication
  |
  +--> RBAC policy checks
  |
  +--> PostgreSQL / Prisma
  |
  +--> Agent coordinator
          |
          +--> role/task agent
          +--> retrieval agent
          +--> workflow agent
                  |
                  v
             Tool registry
                  |
          permitted operations
```

## Security boundary

A core design rule for the lab:

> The model does not decide whether a user is authorized.

Authorization should be enforced by deterministic application code before a tool executes. An agent may request an operation; the application decides whether that operation is permitted for the authenticated user and current context.

## Planned agent responsibilities

### Coordinator

Routes a user request or workflow step to a specialized agent and maintains task context.

### Retrieval agent

Finds relevant synthetic operational knowledge without receiving unnecessary tool permissions.

### Workflow agent

Assists with a guided task and can request explicitly registered actions.

These roles may change during implementation. The point is to experiment with capability boundaries rather than maximize agent count.

## Tool design

Each tool should have:

- a narrow purpose
- typed inputs
- validation
- permission checks
- predictable error output
- an audit-friendly result

Example conceptual tools:

```text
get_customer_record(id)
search_knowledge(query)
create_training_ticket(input)
update_training_ticket(id, patch)
```

All data will be synthetic.

## Data model direction

Likely entities:

- User
- Role
- TrainingScenario
- ScenarioStep
- SyntheticCustomer
- Ticket
- AgentRun
- ToolInvocation

`AgentRun` and `ToolInvocation` records are particularly useful for inspecting what happened during a multi-step interaction.

## Testing strategy

The lab should test more than UI rendering:

- RBAC unit/integration tests
- schema validation for tool inputs
- deterministic tool behavior
- model-response boundary handling
- denied-action scenarios
- tool failures and retries
- end-to-end guided workflow tests with Playwright

## Implementation sequence

1. Scaffold Next.js + TypeScript application
2. Define synthetic domain and Prisma schema
3. Add authentication and role model
4. Build deterministic workflow without AI
5. Add tool registry and authorization boundary
6. Integrate Claude for one narrowly scoped agent workflow
7. Add run/tool audit records
8. Add tests for denied and failed operations
9. Add additional agents only where specialization improves the design
10. Publish demo screenshots and an architecture retrospective

## Non-goals

- Recreating any client application
- Reusing proprietary prompts or source code
- Maximizing the number of agents
- Treating LLM output as an authorization mechanism
- Building an impressive demo at the expense of understandable architecture
