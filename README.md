# Harness Engineering

**Harness Engineering** is the engineering discipline of building the
environment around an AI model so that the model can perform complex
tasks reliably, repeatedly, safely, and measurably.

A simple mental model is:

``` text
LLM / Model
    |
    v
+---------------------------+
|      AGENT HARNESS        |
|                           |
| Context + Memory          |
| Tools + APIs              |
| Planning + Orchestration  |
| Permissions + Guardrails  |
| Execution + Verification  |
| Monitoring + Evaluation   |
+-------------+-------------+
              |
              v
         Real World
```

The model provides reasoning and language capabilities. The harness
provides the environment, tools, control, state, execution, feedback,
and safety mechanisms required to turn that capability into useful work.

------------------------------------------------------------------------

# 1. What Is Harness Engineering?

## Simple Definition

> **Harness Engineering is the practice of designing the environment
> around an AI model --- context, tools, state, orchestration,
> permissions, execution, verification, and feedback --- so that an
> agent can reliably accomplish real-world tasks.**

A useful formula is:

``` text
Agent = Model + Harness
```

A production-oriented formula is:

``` text
Reliable Agent
=
Model
+
Context
+
Tools
+
Orchestration
+
State
+
Permissions
+
Execution Environment
+
Verification
+
Observability
+
Evaluation
+
Recovery
```

------------------------------------------------------------------------

# 2. Why Is It Called a "Harness"?

Think about a horse.

A horse provides physical power, but a rider needs a harness, reins,
direction, boundaries, and feedback to control that power.

Similarly:

``` text
Horse                  AI System
------------------------------------------------
Power                   Model intelligence
Harness                 Agent harness
Reins                   Policies / controls
Rider                   User / developer
Environment             Tools / runtime
Direction               Instructions / planning
Feedback                Observability / evaluation
```

The model is powerful, but it needs an engineered environment to perform
useful work reliably.

------------------------------------------------------------------------

# 3. LLM vs Agent vs Harness

## 3.1 LLM

A basic LLM interaction is:

``` text
User
  |
  v
Prompt
  |
  v
LLM
  |
  v
Answer
```

Example:

``` text
User:
Explain Redis.

LLM:
Redis is an in-memory data store...
```

The model does not automatically have permission to:

-   inspect your repository
-   modify files
-   execute code
-   query your production database
-   call external APIs
-   remember every previous task
-   deploy applications

------------------------------------------------------------------------

## 3.2 Agent

Give the model tools and an execution loop:

``` text
                 +-- Database
                 +-- API
LLM --> Agent ---+-- Files
                 +-- Browser
                 +-- Code execution
```

Example:

> "Find why my NestJS API returns HTTP 500."

An agent may:

1.  Read source code.
2.  Inspect logs.
3.  Find the relevant service.
4.  Inspect the database query.
5.  Modify code.
6.  Run tests.
7.  Analyze failures.
8.  Fix the code.
9.  Run tests again.
10. Report the result.

------------------------------------------------------------------------

## 3.3 Harness

The harness adds the complete operating environment:

``` text
                    MODEL
                      |
                      v
             +----------------+
             |    HARNESS     |
             +----------------+
             | Context        |
             | Memory         |
             | Tools          |
             | Planning       |
             | State          |
             | Permissions    |
             | Guardrails     |
             | Execution      |
             | Verification   |
             | Recovery       |
             | Observability  |
             | Evaluation     |
             +--------+-------+
                      |
                      v
                Real World
```

This is the key difference between a simple chatbot and a
production-oriented agent system.

------------------------------------------------------------------------

# 4. Engineering Hierarchy

The attachment describes three increasingly broad levels:

``` text
Prompt Engineering
        |
        v
Context Engineering
        |
        v
Harness Engineering
```

## 4.1 Prompt Engineering

Prompt Engineering deals primarily with instructions.

Example:

``` text
"Create a NestJS authentication service.
Use JWT and PostgreSQL."
```

It is essentially:

``` text
Instruction -> Model -> Output
```

------------------------------------------------------------------------

## 4.2 Context Engineering

Context Engineering provides the model with the information it needs.

Example:

``` text
Task
+
Project documentation
+
Database schema
+
API specification
+
Previous state
+
Relevant source files
+
Retrieved documents
        |
        v
      Model
```

The model does not need to guess the architecture.

------------------------------------------------------------------------

## 4.3 Harness Engineering

Harness Engineering adds the complete environment:

``` text
Context
+
Tools
+
MCP
+
Code execution
+
Browser
+
Planning
+
Loops
+
Memory
+
Permissions
+
Validation
+
Security
+
Observability
+
Evaluation
+
Recovery
```

------------------------------------------------------------------------

# 5. The Five Pillars of Harness Engineering

The attached diagram identifies five important pillars:

1.  Context --- Eyes and Memory
2.  Action --- Hands and Limbs
3.  Orchestration --- Nervous System
4.  Control --- Immune System
5.  Feedback --- Vitals

These provide a useful mental model for designing an agent harness.

------------------------------------------------------------------------

# 6. Pillar 1 --- Context

## Context = Eyes + Memory

Context answers:

> **What does the agent know right now?**

Context may contain:

``` text
User request
+
Instructions
+
Conversation
+
Files
+
RAG results
+
Database information
+
API results
+
Previous actions
+
Current state
```

------------------------------------------------------------------------

## 6.1 Memory

Memory stores useful information across interactions.

Example:

``` text
User:
My preferred database is PostgreSQL.

Later:

Agent:
I will use PostgreSQL for this implementation.
```

Memory can be:

-   short-term conversation memory
-   task state
-   long-term user preferences
-   application state
-   summarized history

------------------------------------------------------------------------

## 6.2 RAG

RAG means **Retrieval-Augmented Generation**.

Instead of putting millions of documents into the model context:

``` text
10,000,000 documents
        |
        v
    Retriever
        |
        v
Top relevant documents
        |
        v
       LLM
```

Example:

``` text
Question:
"What is our refund policy?"

Retriever:
Finds refund-policy.pdf

LLM:
Uses the retrieved content to answer.
```

RAG is a component of a harness, not a complete harness.

------------------------------------------------------------------------

## 6.3 Retrieval Knowledge

Useful retrieval sources can include:

-   internal documentation
-   database records
-   API responses
-   source code
-   product manuals
-   knowledge bases
-   previous task results

------------------------------------------------------------------------

## 6.4 Instructions

Instructions define behavior and constraints.

Example:

``` text
You are a customer support agent.

Rules:
1. Verify customer identity.
2. Never expose internal information.
3. Do not issue refunds above ₹10,000 automatically.
4. Ask for approval for larger refunds.
```

Important:

> Critical security and business rules should be enforced by software,
> not only by prompts.

------------------------------------------------------------------------

# 7. Pillar 2 --- Action

## Action = Hands + Limbs

Action answers:

> **What can the agent actually do?**

Typical tools include:

``` text
Database
API
Browser
File system
Shell
Email
CRM
Payment API
Git
Docker
Code execution
MCP
```

Example:

``` text
Agent:
"I need to check the customer's order."

        |
        v

getOrder(orderId)

        |
        v

Database

        |
        v

Order result
```

------------------------------------------------------------------------

# 8. Tool Design

Good tools should be:

-   narrowly scoped
-   predictable
-   typed
-   documented
-   validated
-   permission controlled
-   observable

Example:

``` typescript
getOrder({
  orderId: string
})
```

Returns:

``` json
{
  "id": "ORD-1001",
  "status": "cancelled",
  "reason": "payment_timeout"
}
```

Avoid exposing a huge collection of ambiguous tools.

------------------------------------------------------------------------

# 9. MCP

**MCP (Model Context Protocol)** provides a standardized mechanism for
AI applications to connect to external tools and data sources.

Conceptually:

``` text
              Agent
                |
               MCP
        +-------+-------+
        |       |       |
       GitHub  DB     Files
```

MCP can be used as an integration/action layer inside a larger harness.

Important distinction:

``` text
Harness != MCP
```

MCP can be one component of a harness.

------------------------------------------------------------------------

# 10. Code Execution and Browser Access

Coding and research agents often need execution capabilities.

Example:

``` text
User:
Analyze this CSV and create a report.

Agent:
1. Read CSV
2. Write Python
3. Execute Python
4. Inspect output
5. Detect anomalies
6. Generate report
```

The model itself is not the execution environment.

The harness provides the execution environment.

------------------------------------------------------------------------

# 11. Pillar 3 --- Orchestration

## Orchestration = Nervous System

Orchestration answers:

> **What should happen next?**

Suppose the user asks:

> "Build a complete authentication system."

The task can be decomposed:

``` text
Main Task
|
+-- Analyze existing project
|
+-- Design authentication
|
+-- Create database changes
|
+-- Implement backend
|
+-- Implement frontend
|
+-- Write tests
|
+-- Run tests
|
+-- Verify
```

------------------------------------------------------------------------

# 12. Planning and Agent Loops

A common agent loop is:

``` text
PLAN
 |
 v
ACT
 |
 v
OBSERVE
 |
 v
CHECK
 |
 +---- FAIL ----> CORRECT
 |                  |
 +---- PASS <-------+
 |
 v
COMPLETE
```

For coding:

``` text
Write code
   |
Run tests
   |
Tests fail
   |
Analyze failure
   |
Fix code
   |
Run tests again
   |
Tests pass
   |
Finish
```

------------------------------------------------------------------------

# 13. Workflow and Task Decomposition

Not every operation needs an LLM.

Example:

``` text
Receive ticket
      |
      v
Classify
      |
      v
Retrieve customer
      |
      v
Analyze issue
      |
      v
Check policy
      |
      v
Approval required?
   /          \
 NO            YES
 |              |
 v              v
Refund        Human
 |            Approval
 v              |
Notify <---------+
```

A strong design principle is:

> **Use deterministic code where deterministic code is enough. Use an
> LLM where reasoning is valuable.**

------------------------------------------------------------------------

# 14. State Management

Long-running agents need state.

Example:

``` text
Task ID: TASK-123

Status:
ANALYSIS_COMPLETE

Completed:
[x] Repository scanned
[x] Architecture understood
[x] Database inspected

Pending:
[ ] Implement service
[ ] Write tests
[ ] Run tests
```

Possible persistence:

``` text
PostgreSQL
Redis
Object Storage
Event Store
```

------------------------------------------------------------------------

# 15. Sub-Agents

A larger system may use specialized agents:

``` text
                 Main Agent
                     |
       +-------------+-------------+
       |             |             |
       v             v             v
 Researcher       Coder         Tester
       |             |             |
       +-------------+-------------+
                     |
                     v
                  Reviewer
```

But do not create multiple agents just because you can.

Often:

``` text
1 agent + good tools
```

is simpler and more reliable than:

``` text
10 agents + complicated coordination
```

------------------------------------------------------------------------

# 16. Pillar 4 --- Control

## Control = Immune System

Control answers:

> **What is the agent allowed to do?**

Suppose an agent has:

``` text
readDatabase()
updateDatabase()
deleteDatabase()
sendEmail()
issueRefund()
deployProduction()
```

Do not necessarily give every operation unrestricted access.

Example policy:

``` text
READ database       -> allowed
UPDATE database     -> validation
DELETE database     -> approval
REFUND > ₹10,000    -> human approval
PRODUCTION DEPLOY   -> human approval
```

------------------------------------------------------------------------

# 17. Guardrails and Permissions

Guardrails can control:

-   allowed tools
-   allowed parameters
-   allowed data
-   allowed users
-   allowed environments
-   allowed operations
-   allowed network destinations

For a multi-tenant SaaS:

``` text
Tenant A Agent
      |
      +--> Tenant A data only

Tenant B Agent
      |
      +--> Tenant B data only
```

Do not rely only on a prompt such as:

> "Do not access another tenant."

Enforce tenant isolation in your database and authorization layer.

------------------------------------------------------------------------

# 18. Validation

Never blindly trust LLM output.

Suppose the model returns:

``` json
{
  "amount": -5000
}
```

Application validation should reject it:

``` typescript
if (amount <= 0) {
  throw new ValidationError();
}
```

This is a fundamental harness principle:

> **Important constraints should be enforced by software, not merely
> described in a prompt.**

------------------------------------------------------------------------

# 19. Human-in-the-Loop

For risky operations:

``` text
Agent
 |
 v
Risky operation
 |
 v
Policy Engine
 |
 v
Human approval required
 |
 +---- Approve
 |
 +---- Reject
```

Example:

``` text
AI can:
[x] Analyze refund request

AI cannot:
[ ] Issue a large refund without approval
```

------------------------------------------------------------------------

# 20. Security

A production harness should consider:

-   authentication
-   authorization
-   tenant isolation
-   secrets management
-   sandboxing
-   network restrictions
-   filesystem permissions
-   tool permissions
-   prompt injection
-   data leakage
-   audit logs
-   rate limits
-   resource limits

------------------------------------------------------------------------

# 21. Pillar 5 --- Feedback

## Feedback = Vitals

Feedback answers:

> **How do we know whether the agent is working correctly?**

Important feedback mechanisms include:

-   logs
-   traces
-   metrics
-   evaluation
-   error signals
-   latency
-   cost
-   tool success/failure
-   human feedback

------------------------------------------------------------------------

# 22. Logs and Monitoring

Track information such as:

``` text
Task ID
Agent ID
Model
Prompt/version
Tools called
Tool results
Tokens
Latency
Errors
Retries
Final result
```

Example:

``` text
TASK-123

Model calls:       7
Tool calls:        12
Duration:          48 sec
Tokens:            18,400
Retries:           2
Final status:      SUCCESS
```

------------------------------------------------------------------------

# 23. Tracing

A trace can show the complete execution path:

``` text
Task
 |
 +-- LLM call
 |
 +-- Search tool
 |      |
 |      +-- Database query
 |
 +-- LLM call
 |
 +-- Code execution
 |      |
 |      +-- npm test
 |
 +-- Error
 |
 +-- LLM recovery
 |
 +-- npm test
        |
        +-- SUCCESS
```

Tracing helps answer:

> Why did the agent succeed or fail?

------------------------------------------------------------------------

# 24. Evaluation

Agent systems require systematic evaluation.

Example test cases:

``` text
Test 1:
Customer asks refund
Expected:
Correct policy

Test 2:
Customer asks for another customer's data
Expected:
DENY

Test 3:
Invalid order ID
Expected:
Proper error

Test 4:
Payment API unavailable
Expected:
Retry/recovery
```

You can maintain an evaluation dataset:

``` json
[
  {
    "input": "Find order 100",
    "expected": "Order returned"
  },
  {
    "input": "Delete another user's data",
    "expected": "Denied"
  }
]
```

Run the harness against the dataset after major changes.

------------------------------------------------------------------------

# 25. Error Signals and Latency

An agent may be technically correct but still unusable.

Example:

``` text
Correctness:       95%
Average latency:   45 sec
Cost/request:      ₹8
Retries:           3
```

Harness engineering optimizes the entire system, not only model
accuracy.

------------------------------------------------------------------------

# 26. Industry Examples

The modern ecosystem contains systems that implement overlapping parts
of the harness concept.

## 26.1 OpenAI

OpenAI provides multiple approaches:

-   Agents API
-   Agents SDK
-   Codex SDK / Codex harness capabilities

Conceptually:

``` text
Application
    |
    v
Agent API / SDK
    |
    +-- Model
    +-- Tools
    +-- Orchestration
    +-- Sessions
    +-- Guardrails
    +-- Approvals
    +-- Tracing
```

------------------------------------------------------------------------

## 26.2 DeepSeek Harness

DeepSeek Harness is a plugin-oriented open-source harness.

A simplified architecture:

``` text
DeepSeek Harness
|
+-- Model Plugin
+-- Tool Plugin
+-- Session Plugin
+-- Storage Plugin
+-- Sandbox Plugin
+-- Loop Plugin
+-- Skill Plugin
+-- UI Plugin
```

The central philosophy is:

> **Everything is a plugin.**

------------------------------------------------------------------------

## 26.3 Microsoft Agent Framework

Microsoft Agent Framework includes agents, tools, workflows, sessions,
middleware, safety and harness capabilities.

A simplified view:

``` text
Agents
+
Tools
+
Sessions
+
Memory
+
Workflows
+
Middleware
+
Safety
+
Harness
+
Evaluation
+
Observability
```

------------------------------------------------------------------------

## 26.4 LangGraph

LangGraph is useful when you need explicit control over stateful
workflows.

Example:

``` text
START
  |
  v
Research
  |
  v
Analyze
  |
  v
Need approval?
 /       \
YES       NO
 |         |
Human      |
 |         |
 +----+----+
      |
      v
    Write
      |
     END
```

Important capabilities include:

-   state
-   graph workflows
-   persistence
-   durable execution
-   human-in-the-loop
-   streaming

------------------------------------------------------------------------

## 26.5 CrewAI

CrewAI provides two important abstractions:

``` text
Crew
 |
 +-- Multiple agents
```

and:

``` text
Flow
 |
 +-- Structured workflow
```

Example:

``` text
Researcher
    |
    v
Writer
    |
    v
Reviewer
    |
    v
Publisher
```

------------------------------------------------------------------------

## 26.6 Claude Agent SDK

Claude's agent-oriented SDK supports computer-use-style workflows
involving capabilities such as:

-   files
-   shell
-   code execution
-   tools
-   iterative agent loops

Example:

``` text
"Fix the failing tests."

        |
        v
Inspect repository
        |
        v
Run tests
        |
        v
Read failure
        |
        v
Edit code
        |
        v
Run tests
        |
        +---- FAIL -> Fix again
        |
        +---- PASS -> Finish
```

------------------------------------------------------------------------

## 26.7 Google ADK

Google's Agent Development Kit provides agent, tool, workflow, callback
and runtime capabilities.

Simplified architecture:

``` text
Agent
|
+-- Model
+-- Tools
+-- Memory
+-- Workflow
+-- Callbacks
+-- Runtime
```

------------------------------------------------------------------------

# 27. Harness / Agent Framework Ecosystem

As of 2026, relevant options include:

  ------------------------------------------------------------------------
  Framework / Platform    Type                    Main Focus
  ----------------------- ----------------------- ------------------------
  OpenAI Agents API       Managed                 Managed agent/Codex
                                                  harness capabilities

  OpenAI Agents SDK       Open source SDK         Application-controlled
                                                  agents

  Codex SDK               SDK/runtime             Run coding-agent
                                                  harnesses in your
                                                  environment

  DeepSeek Harness        Open source             Plugin-based harness

  Microsoft Agent         Open source/framework   Agents + workflows +
  Framework                                       harness

  LangGraph               Open source             Stateful graph
                                                  orchestration

  CrewAI                  Open source/framework   Multi-agent crews +
                                                  flows

  Claude Agent SDK        SDK                     Computer-oriented agent
                                                  loop

  Google ADK              Open source/framework   Agents + tools +
                                                  workflows

  Custom Harness          Custom                  Full control
  ------------------------------------------------------------------------

The terminology overlaps: not every framework calls itself a "harness",
but many provide components that make up a harness.

------------------------------------------------------------------------

# 28. Where to Use Harness Engineering

Harness engineering is especially useful for tasks that are:

-   multi-step
-   long-running
-   tool-heavy
-   stateful
-   expensive
-   risky
-   autonomous
-   difficult to verify manually

Common use cases:

### Software Development

``` text
Issue
 |
 v
Research
 |
 v
Code
 |
 v
Test
 |
 v
Review
 |
 v
PR
```

### Customer Support

``` text
Question
 |
 v
Retrieve customer
 |
 v
Retrieve policy
 |
 v
Analyze
 |
 v
Take action
 |
 v
Verify
```

### Data Analysis

``` text
CSV
 |
 v
Inspect
 |
 v
Write Python
 |
 v
Execute
 |
 v
Analyze
 |
 v
Visualize
 |
 v
Report
```

### Research

``` text
Question
 |
 v
Search
 |
 v
Retrieve
 |
 v
Read
 |
 v
Compare
 |
 v
Verify
 |
 v
Report
```

### DevOps

``` text
Alert
 |
 v
Inspect logs
 |
 v
Check metrics
 |
 v
Diagnose
 |
 v
Propose fix
 |
 v
Approval
 |
 v
Deploy
 |
 v
Verify
```

------------------------------------------------------------------------

# 29. Where Not to Use a Full Harness

Do not build a huge agent system for a simple deterministic problem.

Example:

``` text
"Convert USD to INR."
```

A simple flow is enough:

``` text
Input
 |
 v
FX API
 |
 v
Output
```

You probably do not need:

``` text
12 agents
+
RAG
+
memory
+
planner
+
MCP
+
vector database
+
sub-agent system
```

Avoid overengineering.

------------------------------------------------------------------------

# 30. How to Build Your Own Harness

For a Node.js/NestJS developer, a practical architecture is:

``` text
Next.js
   |
   v
NestJS Agent API
   |
   +-- Harness
   +-- LLM Adapter
   +-- Context Manager
   +-- Tool Registry
   +-- Orchestrator
   +-- Policy Engine
   +-- Memory
   +-- Execution Sandbox
   +-- Verification
   +-- Observability
   |
   +-- PostgreSQL
   +-- Redis
   +-- Object Storage
```

------------------------------------------------------------------------

# 31. Suggested Project Structure

``` text
apps/
|
+-- api/
|   +-- NestJS
|
+-- web/
|   +-- Next.js
|
+-- worker/
    +-- Agent execution
```

Backend:

``` text
src/
|
+-- harness/
|   +-- harness.service.ts
|   +-- harness.types.ts
|   +-- harness.loop.ts
|   +-- harness.module.ts
|
+-- agents/
|   +-- agent.service.ts
|   +-- agent.types.ts
|   +-- agent.module.ts
|
+-- context/
|   +-- context-builder.service.ts
|   +-- memory.service.ts
|   +-- retrieval.service.ts
|   +-- context.module.ts
|
+-- tools/
|   +-- tool-registry.service.ts
|   +-- database.tool.ts
|   +-- github.tool.ts
|   +-- search.tool.ts
|
+-- orchestration/
|   +-- planner.service.ts
|   +-- task.service.ts
|   +-- subagent.service.ts
|
+-- control/
|   +-- policy.service.ts
|   +-- permission.service.ts
|   +-- approval.service.ts
|   +-- guardrail.service.ts
|
+-- execution/
|   +-- sandbox.service.ts
|   +-- executor.service.ts
|
+-- verification/
|   +-- validator.service.ts
|   +-- evaluator.service.ts
|   +-- verifier.service.ts
|
+-- observability/
    +-- tracing.service.ts
    +-- metrics.service.ts
    +-- logging.service.ts
```

------------------------------------------------------------------------

# 32. The Core Harness Loop

The heart of the harness can be represented as:

``` typescript
async function runHarness(task: string) {

  const context = await contextManager.build(task);

  let state = {
    task,
    context,
    status: "running",
  };

  while (!isComplete(state)) {

    const decision = await model.decide({
      task,
      context: state.context,
      tools: toolRegistry.available(),
      state,
    });

    await policyEngine.check(decision);

    const result = await executor.execute(decision);

    state = await stateManager.update(
      state,
      result
    );

    const verification =
      await verifier.check(state);

    if (!verification.success) {
      state = await recovery.handle(
        state,
        verification
      );
    }

    await observability.record(state);
  }

  return state;
}
```

This is the core execution engine.

------------------------------------------------------------------------

# 33. Complete Harness Architecture

``` text
                     USER
                       |
                       v
                +--------------+
                | Task Parser  |
                +------+-------+
                       |
                       v
                +--------------+
                |    Context   |
                |    Builder   |
                +------+-------+
                       |
                       v
                +--------------+
                |     Model    |
                +------+-------+
                       |
                       v
                +--------------+
                |   Planner    |
                +------+-------+
                       |
                       v
                +--------------+
                | Policy Engine|
                +------+-------+
                       |
                       v
                +--------------+
                | Tool Runner  |
                +------+-------+
                       |
                       v
             +--------------------+
             | External World     |
             | DB/API/File/etc.   |
             +---------+----------+
                       |
                       v
                +--------------+
                | Observation  |
                +------+-------+
                       |
                       v
                +--------------+
                | Verification |
                +------+-------+
                       |
                 +-----+-----+
                 |           |
                FAIL        PASS
                 |           |
                 v           v
              Recovery    Complete
                 |
                 +----> Loop
```

------------------------------------------------------------------------

# 34. Development Roadmap

Do not build everything at once.

## Level 0 --- Raw LLM

Build:

``` text
NestJS
 |
 v
LLM API
 |
 v
Response
```

Learn:

-   model APIs
-   messages
-   tokens
-   context windows
-   streaming
-   structured output

------------------------------------------------------------------------

## Level 1 --- Basic Agent

Add tools:

``` text
LLM
+
Tool Registry
```

Example:

``` typescript
tools = [
  searchWeb,
  getUser,
  getOrder
];
```

------------------------------------------------------------------------

## Level 2 --- Context Engineering

Add:

``` text
Context Builder
+
RAG
+
Conversation history
+
Project information
```

------------------------------------------------------------------------

## Level 3 --- Agent Loop

Implement:

``` text
Think
 |
 v
Tool
 |
 v
Observe
 |
 v
Think
 |
 v
Tool
 |
 v
Observe
```

Use an iteration limit:

``` typescript
const MAX_ITERATIONS = 20;
```

Never allow an uncontrolled infinite loop.

------------------------------------------------------------------------

## Level 4 --- State

Add:

``` text
PostgreSQL
+
Redis
```

Store:

``` text
agent_run
task
state
messages
tool_calls
tool_results
status
```

Example:

``` text
agent_runs
----------------
id
user_id
task
status
started_at
completed_at
```

------------------------------------------------------------------------

## Level 5 --- Planning

Add:

``` text
Planner
Task Manager
Todo State
```

Example:

``` json
{
  "tasks": [
    {
      "id": 1,
      "name": "Inspect repository",
      "status": "completed"
    },
    {
      "id": 2,
      "name": "Implement API",
      "status": "running"
    }
  ]
}
```

------------------------------------------------------------------------

## Level 6 --- Permissions

Introduce:

``` text
Policy Engine
```

Example:

``` typescript
if (
  tool === "deleteDatabase" &&
  !user.isAdmin
) {
  throw new PermissionDenied();
}
```

------------------------------------------------------------------------

## Level 7 --- Human Approval

``` text
Agent
 |
 v
Risky operation
 |
 v
Approval request
 |
 v
User
 +-- Approve
 +-- Reject
```

------------------------------------------------------------------------

## Level 8 --- Sandbox

For coding agents:

``` text
Agent
 |
 v
Docker container
 |
 v
Code execution
 |
 v
Tests
```

Avoid allowing unrestricted agents to run arbitrary production commands.

------------------------------------------------------------------------

## Level 9 --- Verification

Add:

``` text
Validator
+
Tests
+
Assertions
+
Business rules
```

For coding agents:

``` text
npm test
npm run lint
npm run build
```

The agent should not simply say "Done" without evidence of completion.

------------------------------------------------------------------------

## Level 10 --- Observability

Add:

``` text
OpenTelemetry
+
Structured logs
+
Traces
+
Metrics
```

Track:

``` text
Latency
Token usage
Cost
Tool success rate
Tool failure rate
Retries
Completion rate
Human approval rate
```

------------------------------------------------------------------------

## Level 11 --- Evaluation

Create evaluation cases:

``` json
[
  {
    "input": "Find order 100",
    "expected": "Order returned"
  },
  {
    "input": "Delete another user's data",
    "expected": "Denied"
  }
]
```

Run them after changes.

The goal is regression measurement.

------------------------------------------------------------------------

## Level 12 --- Self-Improving Harness

Advanced harnesses can analyze failures:

``` text
Agent failure
     |
     v
Trace analysis
     |
     v
Failure category
     |
     +-- Missing context?
     +-- Missing tool?
     +-- Bad tool schema?
     +-- Bad permission?
     +-- Bad workflow?
     +-- Bad verification?
     |
     v
Harness improvement
```

A useful principle is:

> **Do not immediately blame the model. First investigate whether the
> environment, tools, context, workflow, or verification system was
> inadequate.**

------------------------------------------------------------------------

# 35. AI Software Engineer Harness Example

A particularly useful project is an AI Software Engineer Harness.

User:

> "Add Redis caching to the product API."

Possible flow:

``` text
                         TASK
                          |
                          v
                  Repository Scanner
                          |
                          v
                   Context Builder
                          |
                          v
                       Planner
                          |
              +-----------+-----------+
              |           |           |
              v           v           v
           Analyze      Design      Tests
              |           |           |
              +-----------+-----------+
                          |
                          v
                      Code Agent
                          |
                          v
                      File Tools
                          |
                          v
                       npm test
                          |
                    +-----+-----+
                    |           |
                   FAIL        PASS
                    |           |
                    v           v
                  Repair      Verify
                    |           |
                    +-----+-----+
                          |
                          v
                          PR
```

------------------------------------------------------------------------

# 36. Useful Tools for a Coding Harness

## Repository Tools

``` text
readFile
writeFile
searchCode
listFiles
gitDiff
```

## Development Tools

``` text
npmInstall
npmTest
npmBuild
npmLint
dockerRun
```

## Knowledge Tools

``` text
searchDocs
searchRepository
RAG
```

## Git Tools

``` text
gitStatus
gitDiff
gitCommit
gitCreateBranch
```

## Database Tools

``` text
inspectSchema
runReadQuery
migrationCheck
```

------------------------------------------------------------------------

# 37. Tool Permissions

A sensible permission model:

``` text
readFile       -> automatic
searchCode     -> automatic
npmTest        -> automatic

writeFile      -> automatic in sandbox

gitCommit      -> approval

gitPush        -> approval

productionDB   -> forbidden or approval
```

------------------------------------------------------------------------

# 38. Repository Legibility

One of the most important advanced ideas is making the environment
understandable to agents.

A repository can contain:

``` text
AGENTS.md
ARCHITECTURE.md
CONTRIBUTING.md
docs/
```

Example `AGENTS.md`:

``` text
Project:
Product Management API

Architecture:
NestJS modular architecture.

Database:
PostgreSQL + TypeORM.

Rules:
- Use DTO validation.
- Never access repositories from controllers.
- Services contain business logic.
- All endpoints require Swagger documentation.
- Run tests before completion.
```

The repository becomes part of the harness.

------------------------------------------------------------------------

# 39. Mechanical Enforcement

Instead of relying only on:

``` text
"Please don't import repositories directly
into controllers."
```

Use:

``` text
ESLint
+
Architecture tests
+
CI
```

Then:

``` text
Agent makes wrong import
        |
        v
Lint / CI
        |
        v
FAIL
        |
        v
Agent sees failure
        |
        v
Fix
```

The rule is machine-enforced.

------------------------------------------------------------------------

# 40. Agent Entropy

As AI agents modify software repeatedly, architecture can gradually
degrade.

Example:

``` text
Day 1:
Clean architecture

Day 10:
Duplicate utilities

Day 20:
Unused files

Day 30:
Inconsistent APIs

Day 40:
Dead code

Day 50:
Hard-to-understand project
```

This is architectural entropy.

A harness can include maintenance workflows:

``` text
Detect
 |
 v
Analyze
 |
 v
Clean
 |
 v
Test
 |
 v
Verify
```

Think of this as garbage collection for software architecture.

------------------------------------------------------------------------

# 41. Harness vs Agent Framework vs SDK

These terms overlap, but they are not identical.

``` text
LLM
 |
 v
SDK
 |
 +-- API access
 +-- Model communication
 |
 v
Agent Framework
 |
 +-- Tools
 +-- Agents
 +-- Workflows
 +-- Orchestration
 |
 v
Harness
 |
 +-- Environment
 +-- Context
 +-- Tools
 +-- State
 +-- Policy
 +-- Execution
 +-- Verification
 +-- Feedback
```

A modern framework may provide many of these layers.

------------------------------------------------------------------------

# 42. Harness vs RAG

They are different.

## RAG

``` text
Question
 |
 v
Retrieve documents
 |
 v
LLM
 |
 v
Answer
```

## Harness

``` text
Task
 |
 v
Context
 |
 v
Plan
 |
 v
Tools
 |
 v
Execution
 |
 v
Verification
 |
 v
Recovery
 |
 v
Completion
```

RAG can be one component inside a harness.

------------------------------------------------------------------------

# 43. Harness vs MCP

MCP is not the same as a harness.

``` text
Harness
|
+-- Context
+-- Planner
+-- Policy
+-- State
+-- Verification
|
+-- MCP
     |
     +-- GitHub
     +-- Database
     +-- Files
     +-- Other tools
```

MCP can provide a standardized integration layer inside the harness.

------------------------------------------------------------------------

# 44. Harness vs Fine-Tuning

Fine-tuning changes the model.

Harness Engineering changes the environment around the model.

``` text
Fine-tuning
    |
    v
Model changes

Harness Engineering
    |
    v
Environment changes
```

You can often improve an agent by improving:

``` text
Context
+
Tools
+
Workflow
+
Verification
+
Permissions
```

without retraining the model.

------------------------------------------------------------------------

# 45. The Most Useful Mental Model

Remember these questions:

``` text
Prompt:
"What should you do?"

Context:
"What do you need to know?"

Tools:
"What can you do?"

Orchestration:
"What should happen next?"

Control:
"What are you allowed to do?"

Verification:
"Did you actually succeed?"

Observability:
"What happened?"

Harness:
"How do all of these work together?"
```

------------------------------------------------------------------------

# 46. Production Harness Checklist

## Context

-   [ ] Relevant context retrieval
-   [ ] Context size management
-   [ ] Conversation state
-   [ ] Memory
-   [ ] RAG
-   [ ] Context compaction

## Tools

-   [ ] Typed tools
-   [ ] Tool descriptions
-   [ ] Input validation
-   [ ] Timeouts
-   [ ] Retries
-   [ ] Idempotency

## Orchestration

-   [ ] Planning
-   [ ] Task decomposition
-   [ ] State machine
-   [ ] Loop limits
-   [ ] Sub-agents where useful
-   [ ] Recovery

## Control

-   [ ] Authentication
-   [ ] Authorization
-   [ ] Tenant isolation
-   [ ] Tool permissions
-   [ ] Human approval
-   [ ] Sandboxing
-   [ ] Secret management

## Verification

-   [ ] Output validation
-   [ ] Business rules
-   [ ] Tests
-   [ ] Assertions
-   [ ] Completion criteria

## Feedback

-   [ ] Logs
-   [ ] Metrics
-   [ ] Tracing
-   [ ] Token tracking
-   [ ] Cost tracking
-   [ ] Latency
-   [ ] Error classification
-   [ ] Evaluation datasets

------------------------------------------------------------------------

# 47. Recommended Learning Roadmap

``` text
Phase 1
LLM Fundamentals
|
+-- Tokens
+-- Context window
+-- Tool calling
+-- Structured output
+-- Streaming
        |
        v
Phase 2
Prompt Engineering
        |
        v
Phase 3
Context Engineering
|
+-- RAG
+-- Memory
+-- Retrieval
+-- Context compression
+-- Dynamic context
        |
        v
Phase 4
Agent Fundamentals
|
+-- Agent loop
+-- Tool calling
+-- State
+-- Planning
        |
        v
Phase 5
Harness Engineering
|
+-- Context
+-- Tools
+-- Orchestration
+-- Control
+-- Feedback
        |
        v
Phase 6
Production
|
+-- Sandbox
+-- Security
+-- Permissions
+-- Observability
+-- Evaluation
+-- Recovery
        |
        v
Phase 7
Advanced
|
+-- Multi-agent
+-- Sub-agents
+-- MCP
+-- Durable execution
+-- Long-running agents
+-- Self-improving harnesses
```

------------------------------------------------------------------------

# 48. Final Architecture

The complete concept can be summarized as:

``` text
                     USER
                       |
                       v
                  +---------+
                  |  GOAL   |
                  +----+----+
                       |
                       v
                  +---------+
                  | CONTEXT |
                  +----+----+
                       |
                       v
                  +---------+
                  |  MODEL  |
                  +----+----+
                       |
                       v
                  +---------+
                  | PLANNER |
                  +----+----+
                       |
                       v
                  +---------+
                  | POLICY  |
                  +----+----+
                       |
                       v
                  +---------+
                  |  TOOLS  |
                  +----+----+
                       |
                       v
                  +---------+
                  | EXECUTE |
                  +----+----+
                       |
                       v
                  +---------+
                  | OBSERVE |
                  +----+----+
                       |
                       v
                  +---------+
                  | VERIFY  |
                  +----+----+
                       |
                  +----+----+
                  |         |
                 FAIL      PASS
                  |         |
                  v         v
               RECOVER   COMPLETE
                  |
                  +-----> LOOP
```

------------------------------------------------------------------------

# 49. One-Sentence Definition

> **Harness Engineering is the practice of designing the environment
> around an AI model --- context, tools, state, orchestration,
> permissions, execution, verification, and feedback --- so that an
> agent can reliably accomplish real-world tasks.**

The most important formula to remember is:

``` text
AGENT
=
MODEL
+
HARNESS
```

And the five pillars from the attached diagram are:

``` text
CONTEXT
   +
ACTION
   +
ORCHESTRATION
   +
CONTROL
   +
FEEDBACK
```

Together, they form the foundation of modern production-grade AI agents.

------------------------------------------------------------------------

# 50. Key Takeaways

1.  **An LLM is not automatically an agent.**
2.  **An agent is not automatically a reliable production system.**
3.  **Harness Engineering builds the environment around the model.**
4.  **Context tells the model what it needs to know.**
5.  **Tools give the model the ability to act.**
6.  **Orchestration determines what happens next.**
7.  **Control limits what the agent is allowed to do.**
8.  **Verification determines whether the task actually succeeded.**
9.  **Feedback makes the system observable and improvable.**
10. **RAG, MCP, memory, tools, planning and sub-agents are components
    --- not the entire harness.**
11. **Critical security rules should be enforced in software, not only
    prompts.**
12. **A good harness can improve agent reliability without changing the
    underlying model.**
13. **Start with a simple agent and progressively add state, tools,
    control, verification, observability and evaluation.**
14. **For coding agents, sandboxed execution and automated tests are
    especially important.**
15. **For production systems, the harness should be treated as software
    infrastructure, not just a prompt.**

------------------------------------------------------------------------

## Suggested Practical Project

For a hands-on learning project, build:

**AI Software Engineer Harness**

Stack:

``` text
Frontend:
Next.js + React

Backend:
NestJS + TypeScript

Database:
PostgreSQL + TypeORM

Cache:
Redis

LLM:
Pluggable model adapter

Tools:
File system
Git
Shell
Database
Search

Execution:
Docker sandbox

Integration:
MCP

Security:
RBAC + approval system

Observability:
OpenTelemetry + structured logs

Evaluation:
Automated agent test dataset
```

Build it incrementally:

``` text
LLM
  ->
Tool Calling
  ->
Context
  ->
Agent Loop
  ->
State
  ->
Planning
  ->
Permissions
  ->
Sandbox
  ->
Verification
  ->
Observability
  ->
Evaluation
  ->
Production Harness
```

This project covers almost every major concept in Harness Engineering
while fitting naturally into a modern Node.js/NestJS development
workflow.
