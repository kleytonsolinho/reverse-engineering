---
name: codebase-reverse-engineering
description: Use this skill when the task requires understanding how a project really works by reading the code, reverse engineering third-party projects, mapping entrypoints, flows, dependencies, contracts, structural patterns, and technical causes without assuming anything not supported by direct repository evidence.
metadata:
  priority: 9
  promptSignals:
    phrases:
      - "engenharia reversa"
      - "engenharia reversa completa"
      - "reverse engineer"
      - "reverse engineering"
      - "analise a arquitetura"
      - "analise a arquitetura do repositorio"
      - "entenda como esse repositorio funciona"
      - "mapeie os fluxos"
      - "mapeie os fluxos principais"
      - "gere um relatorio da arquitetura"
      - "gere um relatorio do repositorio"
      - "explique como o sistema funciona na pratica"
      - "entrypoints reais"
      - "fluxos principais"
      - "runtime flow"
      - "onboarding tecnico"
      - "full reverse engineering"
      - "analyze the repository architecture"
      - "map the main flows"
      - "generate a repository report"
      - "explain how this repository works"
      - "ingenieria inversa"
      - "analiza la arquitectura del repositorio"
      - "mapea los flujos principales"
      - "genera un informe del repositorio"
      - "explica como funciona este repositorio"
    allOf:
      - ["engenharia", "reversa"]
      - ["arquitetura", "repositorio"]
      - ["fluxos", "principais"]
      - ["como", "funciona"]
      - ["gere", "relatorio"]
      - ["entrypoints", "reais"]
      - ["reverse", "engineering"]
      - ["repository", "architecture"]
      - ["main", "flows"]
      - ["ingenieria", "inversa"]
      - ["informe", "repositorio"]
    anyOf:
      - "engenharia"
      - "reversa"
      - "arquitetura"
      - "entrypoint"
      - "entrypoints"
      - "fluxos"
      - "runtime"
      - "relatorio"
      - "onboarding"
      - "repositorio"
      - "reverse"
      - "engineering"
      - "architecture"
      - "report"
      - "repository"
      - "ingenieria"
      - "inversa"
      - "arquitectura"
      - "informe"
    minScore: 4
---

# Codebase Reverse Engineering

Use this skill when the goal is to learn, explain, audit, or debug how a repository works in practice.

It is designed especially for projects built by other people, whether AI-assisted or not, when the current team needs a reliable base of knowledge about how that system actually operates.

It exists to answer questions such as:

- where a feature really starts and ends
- what the runtime entrypoint is
- how data crosses layers, modules, and services
- which architectural patterns are in use
- which dependencies are central and which are details
- why a structure was built this way
- where a bug likely starts and how it propagates

## Core Rule

Do not assume. Do not fill gaps with intuition. Do not answer based on generic convention if the repository has not been read yet.

Also do not stop at the first plausible explanation. Whenever a concept, rule, dependency, boundary, or flow seems understood, force new questions about it until you discover how it is actually sustained in the code.

If something is not confirmed in the code, say it explicitly:

- `not confirmed in the code reviewed`
- `I did not find local evidence for this`
- `I need to read more files to close this answer`

## Deep Investigation Mode

Every time this skill finds a new system rule, an important concept, or relevant behavior, it should enter a self-questioning cycle before concluding.

Questions it should ask itself:

- where exactly does this rule originate in the code
- who depends on this rule
- who breaks if this rule changes
- what is the entrypoint for this decision
- where is this rule applied, validated, transformed, or bypassed
- does this apply to the whole system or only to this flow
- is there a contradiction or exception in another file
- is there a composition, adapter, factory, provider, middleware, hook, or controller sustaining this
- what data comes in, what data goes out, and who translates between layers
- what still needs to be read to turn this explanation into complete knowledge

If there is still more depth to extract, keep asking and gathering evidence before responding.

## Read First

- `references/investigation-checklist.md`
- `references/output-contract.md`
- `../shared/references/multilingual-export-pattern.md`

## Process

1. Identify the real operational question.
2. Locate the bootstrap files and entrypoints for the investigated scope.
3. Map flow ownership:
   - who receives the input
   - who transforms it
   - who orchestrates it
   - who integrates with external systems
   - who renders, persists, or publishes it
4. Follow the real code flow using symbols, imports, calls, schemas, routes, handlers, and configuration.
5. For each discovered concept or rule, ask deep and excessive questions to expand understanding before concluding.
6. Build an evidence map with concrete files and excerpts before concluding.
7. Identify structural rules:
   - layers
   - dependency direction
   - contracts
   - factories
   - adapters
   - hooks
   - services
   - use cases
   - entities
8. Identify the structural why behind each important decision:
   - change isolation
   - reuse
   - framework boundary
   - testability
   - controlled coupling
   - runtime composition
9. For debugging, follow the failure from symptom to origin:
   - input
   - intermediate state
   - boundary
   - root cause
10. Consolidate the understanding into a reverse-engineering report for knowledge transfer.
11. Answer only what is supported by the evidence reviewed.
12. Always close with a summary, example, and remaining gaps.

## Guardrails

- Read the code before giving an opinion about architecture.
- Prefer `rg`, reading manifests, configs, routes, schemas, and composition files before opening random files.
- Always deepen discovery with self-questions before calling something understood.
- Do not call something an architectural pattern without pointing to where it appears.
- Do not say a dependency is central without showing where it enters runtime.
- Do not say a module is dead without looking for references.
- Do not say a bug is resolved without explaining the causal chain.
- Do not stop at the flow description without also explaining ownership, contracts, boundaries, and propagation.
- When there is more than one possible flow, separate:
  - `confirmed flow`
  - `unconfirmed hypothesis`

## What This Skill Should Deliver

- direct and objective explanation
- final reverse-engineering report focused on knowledge transfer
- operational onboarding guide for new engineers
- visual architecture and flow artifact in Mermaid
- technical reasoning behind the structure
- concrete repository example
- ASCII graph of flow or dependency when that helps
- end-to-end flow map, from initial input to final output
- structural patterns found and where they appear
- high-signal final summary

## Minimum Response Format

1. `Summary`
2. `How It Works`
3. `Why It Works This Way`
4. `Patterns Found`
5. `Graph`
6. `Concrete Example`
7. `Gaps Or Next Files To Read`

## Required Output Structure

When this skill produces exportable documentation, it should create a folder:

- `reports/<ProjectName>/`

Inside it, generate these three files by default:

1. `REVERSE-ENGINEERING.md`
2. `ONBOARDING-GUIDE.md`
3. `ARCHITECTURE-GRAPHS.md`

## Report Language

- Detect the primary language of the user's request before writing the reports.
- Write the report content in the same language as the user's request.
- Preserve file names in English to maintain the plugin standard.
- If the language is ambiguous or mixed, use the predominant language from the first request.
- If it is still unclear, use English.

### Responsibility Of Each File

- `REVERSE-ENGINEERING.md`
  - primary evidence-based analysis
  - entrypoints
  - flows
  - ownership
  - patterns
  - gaps

- `ONBOARDING-GUIDE.md`
  - guided reading
  - table `file -> responsibility -> when to read`
  - onboarding checklist
  - short goal-based playbooks

- `ARCHITECTURE-GRAPHS.md`
  - Mermaid diagrams separated by view
  - harness-specific flows
  - primary flow
  - execution flow
  - structural map of components and connections

When helpful, `REVERSE-ENGINEERING.md` and `ONBOARDING-GUIDE.md` should point to `ARCHITECTURE-GRAPHS.md` in sections where visualization adds clarity.

## Expected Result

The expected result of this skill is a report that allows engineers to understand:

- how the project starts
- how flows cross layers
- which modules are central
- which contracts and boundaries organize the system
- which patterns truly appear
- where the extension, risk, and coupling points are

And when export is required, that knowledge should be organized repeatably inside `reports/<ProjectName>/`.

The goal is not only to answer a one-off question. The end goal is to build reliable operational knowledge about how the project works.

## Investigation Heuristics

- Start with:
  - `package.json`, `turbo.json`, manifests, framework configs, app bootstrap, route registries, and composition points
- For frontend:
  - start with `app`, `pages`, layouts, providers, services, features, hooks, and contracts
- For backend:
  - start with HTTP bootstrap, routes, controllers, presenters, use cases, entities, repositories, and adapters
- For libraries and packages:
  - start with public exports, factories, registries, adapters, and tests
- For incidents:
  - start from the observable symptom and walk backward through the real flow

## Required Questions Per Discovery

When discovering something important, this skill should try to answer, with evidence, questions such as:

- which file introduces this into runtime
- who calls this
- who is called by this
- which contract supports this exchange
- where this changes form, layer, or responsibility
- which part is business logic and which part is framework detail
- where duplicates, exceptions, or shortcuts exist
- what a new engineer would need to know to avoid misreading this

## When To Combine With Other Skills

- Use `debug` when the task requires systematic bug isolation and root-cause verification.
- Use `explain-code` when the priority is teaching and analogies, not deep mapping.
- Use specialized architecture skills when the repository already has an explicit layer contract.
