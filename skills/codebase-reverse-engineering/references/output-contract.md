# Output Contract

Every response from this skill must follow this minimum contract.

The end goal is to produce a reverse-engineering report that serves as a knowledge base for engineers who need to understand a project built by third parties.

When the task calls for structured export, the output must be organized as:

- `reports/<ProjectName>/REVERSE-ENGINEERING.md`
- `reports/<ProjectName>/ONBOARDING-GUIDE.md`
- `reports/<ProjectName>/ARCHITECTURE-GRAPHS.md`

Text documents should reference the graphs file when visualization helps explain flows, connections, or boundaries.

## 1. Summary

- Answer the main question in direct language.
- State what is confirmed in the code.
- If there is uncertainty, say so explicitly.

## 2. How It Works

- Describe the real flow in order.
- Cover the end-to-end flow, from the initial input to the final output, whenever the scope allows.
- Cite relevant files, modules, symbols, or composition points.
- Separate `confirmed flow` from `unconfirmed hypothesis` when needed.

## 3. Why It Works This Way

- Explain the structure based on repository evidence.
- Point out layers, boundaries, contracts, adapters, factories, or other observed structural rules.
- Do not attribute intent without local evidence.

## 4. Patterns Found

- List the structural patterns actually found in the code.
- For each pattern, say where it appears and why that reading is supported by evidence.
- If there is doubt, mark it explicitly as `not confirmed in the code reviewed`.

## 5. Graph

- Include an ASCII graph when it helps visualize flow, dependencies, or failure propagation.
- Prefer a small, readable graph grounded in the confirmed flow.

Example:

```text
input
  -> route/controller
  -> use-case/service
  -> adapter/repository
  -> persistence or output
```

## 6. Concrete Example

- Show a real path through the repository.
- Use at least one specific file or named snippet to anchor the explanation.

## 7. Gaps Or Next Files To Read

- List what has not yet been confirmed.
- State which files should be read to close the answer.
- Use explicit phrases such as:
  - `not confirmed in the code reviewed`
  - `I did not find local evidence for this`
  - `I need to read more files to close this answer`

## Required Depth

Before concluding, the skill should answer questions like:

- why do I believe this flow starts here
- which file confirms this rule
- which module depends on this
- is there an exception for this behavior
- how does this data change as it crosses layers
- what has not yet been explained about this section

If those questions open new relevant trails, the skill should investigate further before closing the report.

## Visual Artifacts

- Generate Mermaid diagrams when the system structure, harness-specific flows, boundaries, or connections become clearer visually.
- If the diagrams become long or reusable, extract them into `ARCHITECTURE-GRAPHS.md`.
- In `REVERSE-ENGINEERING.md` and `ONBOARDING-GUIDE.md`, point explicitly to `ARCHITECTURE-GRAPHS.md` when that helps.
