# Reverse Engineering

When the user asks for reverse engineering, architecture analysis, runtime mapping, onboarding documentation, or a technical explanation of how a repository really works, treat this plugin as the primary workflow.

## Mandatory behavior

- Investigate the repository directly from code before concluding.
- Do not answer with a loose summary when the user asked for a full reverse engineering.
- Create the export folder in the repository using the standard structure:
  - `reports/<ProjectName>/REVERSE-ENGINEERING.md`
  - `reports/<ProjectName>/ONBOARDING-GUIDE.md`
  - `reports/<ProjectName>/ARCHITECTURE-GRAPHS.md`
- Keep file names fixed in English.
- Write the report content in the same language as the user's request.

## Routing

If the request is broad and natural-language, use the `reverse-engineering` skill as the entrypoint.

If the task is already clearly a deep repository investigation, use `codebase-reverse-engineering`.

## Output expectation

A correct completion for a full reverse engineering request is not only an explanation in chat.

A correct completion is:

1. investigate the codebase
2. create the report artifacts
3. answer based on the generated artifacts
