# Investigation Checklist

Use this checklist before concluding any analysis.

## 1. Operational Question

- What real question needs to be answered?
- Is the goal to explain architecture, find the entrypoint, trace a flow, or debug a bug?
- Is the scope clear: feature, module, request, screen, job, command, or incident?

## 2. Bootstrap And Entrypoints

- Did I read the main manifests?
- Did I read the relevant bootstrap files?
- Did I identify where this flow enters runtime?
- Did I separate a confirmed entrypoint from one that is only suspected?

## 3. Real Flow

- Who receives the input?
- Who validates it?
- Who transforms it?
- Who orchestrates it?
- Who calls external integrations?
- Who persists, renders, or publishes it?

## 4. Deep Self-Questions

- For each discovered rule, did I ask where it originates?
- Did I ask who depends on it and who would break if it changed?
- Did I ask whether it applies to the whole system or only this flow?
- Did I look for exceptions, contradictions, or forks of that rule?
- Did I look for the contract, boundary, or adapter that supports this behavior?
- Did I keep investigating until I stopped finding new relevant questions?

## 5. Concrete Evidence

- Do I have specific files to support each important claim?
- Do I have symbols, imports, calls, routes, schemas, or configs that prove the flow?
- Am I describing what I read or filling gaps with intuition?

## 6. Structure

- Which layers actually appear in the code?
- What is the dependency direction between them?
- Are there contracts, interfaces, adapters, factories, or registries?
- Where does the framework end and where does business logic begin?

## 7. Technical Causality

- If I am talking about a bug, did I trace the symptom to its origin?
- If I am talking about architecture, did I explain the structural why based on the code?
- Did I clearly mark what is `confirmed flow` and what is `unconfirmed hypothesis`?

## 8. Closeout

- Does the response end as a reverse-engineering report useful to other engineers?
- Does the response cover the end-to-end flow, patterns found, and remaining gaps?
- If there is export, was the `reports/<ProjectName>/` structure created?
- Were the three standard files generated when applicable?
- Is everything I am claiming confirmed in the reviewed code?
- If not, did I say explicitly that I did not confirm it?
