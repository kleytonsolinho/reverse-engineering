---
name: reverse-engineering
description: Use this skill when the user asks for reverse engineering, architecture analysis, entrypoint mapping, deep repository understanding, or a technical report about how the system works in practice.
metadata:
  priority: 10
  promptSignals:
    phrases:
      - "faça uma engenharia reversa completa"
      - "faca uma engenharia reversa completa"
      - "faça uma engenharia reversa"
      - "faca uma engenharia reversa"
      - "engenharia reversa desse repositorio"
      - "engenharia reversa deste repositorio"
      - "reverse engineer this repository"
      - "reverse engineering deste repositorio"
      - "analise a arquitetura desse repositorio"
      - "analise a arquitetura deste repositorio"
      - "entenda como esse repositorio funciona"
      - "entenda como este repositorio funciona"
      - "gere um relatorio da arquitetura"
      - "gere um relatorio tecnico"
      - "mapeie os fluxos principais"
      - "mostre como o sistema funciona na pratica"
      - "do a full reverse engineering of this repository"
      - "reverse engineer this repository"
      - "analyze the architecture of this repository"
      - "map the main flows of this repository"
      - "generate a technical report for this repository"
      - "show how this system works in practice"
      - "haz una ingenieria inversa completa de este repositorio"
      - "haz una ingenieria inversa de este repositorio"
      - "analiza la arquitectura de este repositorio"
      - "mapea los flujos principales de este repositorio"
      - "genera un informe tecnico de este repositorio"
      - "explica como funciona este sistema en la practica"
    allOf:
      - ["engenharia", "reversa"]
      - ["arquitetura", "repositorio"]
      - ["como", "funciona"]
      - ["gere", "relatorio"]
      - ["fluxos", "principais"]
      - ["reverse", "engineer"]
      - ["technical", "report"]
      - ["main", "flows"]
      - ["ingenieria", "inversa"]
      - ["informe", "tecnico"]
    anyOf:
      - "engenharia reversa"
      - "arquitetura"
      - "entrypoints"
      - "fluxos"
      - "relatorio"
      - "repositorio"
      - "runtime"
      - "onboarding"
      - "reverse engineering"
      - "architecture"
      - "report"
      - "repository"
      - "engineering"
      - "ingenieria inversa"
      - "arquitectura"
      - "informe"
      - "repositorio"
    minScore: 3
---

# Reverse Engineering

When the user asks for reverse engineering of a repository, this skill should take ownership of the full workflow.

Do not wait for additional instructions about:

- how to investigate
- which files to read first
- which export format to use
- which report structure to use

You should lead the investigation and deliver the result using this plugin's official standard.

## What To Do

1. Understand how the repository actually works by reading the code.
2. Locate bootstrap files, entrypoints, and real composition points.
3. Trace end-to-end flows using concrete evidence.
4. Identify ownership, contracts, boundaries, adapters, and structural patterns.
5. Clearly separate:
   - `confirmed flow`
   - `unconfirmed hypothesis`
6. Export the result to:
   - `reports/<ProjectName>/REVERSE-ENGINEERING.md`
   - `reports/<ProjectName>/ONBOARDING-GUIDE.md`
   - `reports/<ProjectName>/ARCHITECTURE-GRAPHS.md`

## Language

- Detect the primary language of the user's request.
- Write all three reports in the same language as the user's request.
- Keep exported file names fixed:
  - `REVERSE-ENGINEERING.md`
  - `ONBOARDING-GUIDE.md`
  - `ARCHITECTURE-GRAPHS.md`
- If the user mixes languages, use the predominant language from the initial request.
- If the language is unclear, use English.

## Required Behavior

- Do not assume anything without local evidence.
- Do not answer with loose prose only when the request is for full reverse engineering.
- Do not stop at a short summary if the request implies structural repository mapping.
- If the user does not specify the project name for the `reports/` folder, derive a reasonable name from the current repository.
- Accept natural requests in Portuguese, English, and Spanish without requiring the skill name.

## Execution Flow

This skill should execute the primary methodology defined in `../codebase-reverse-engineering/SKILL.md`.

Before concluding:

- read `../codebase-reverse-engineering/references/investigation-checklist.md`
- follow the contract in `../codebase-reverse-engineering/references/output-contract.md`
- follow the language pattern in `../shared/references/multilingual-export-pattern.md`
- produce the three export files using the official structure

## Expected Delivery

If the user asks for reverse engineering of this repository, the correct response is not just to explain it.

The correct response is:

1. investigate
2. export
3. answer based on the generated material
