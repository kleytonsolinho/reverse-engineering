# Multilingual Export Pattern

Use this pattern when a skill or agent needs to accept requests in different languages while still producing structured artifacts in a fixed format.

## Goal

Allow the user to speak naturally in their own language without having to learn the plugin's technical names, while keeping the export structure deterministic.

## Rules

1. Detect the primary language of the user's initial request.
2. Respond to the user in that same predominant language.
3. Write the contents of exported artifacts in the same language as the initial request.
4. Keep file names, slugs, technical ids, and structural paths fixed.
5. If the request mixes languages, choose the predominant language from the first relevant request.
6. If the language is unclear, use English as the fallback.

## What Stays Localized

- introductions
- explanations
- tables
- checklists
- narrative examples
- section titles inside the reports

## What Stays Fixed

- file names
- skill names
- technical ids
- folder names
- configuration keys
- export paths

## Example

Request in Portuguese:

- export path:
  - `reports/MyProject/REVERSE-ENGINEERING.md`
- report language:
  - Portuguese

Request in Spanish:

- export path:
  - `reports/MyProject/ONBOARDING-GUIDE.md`
- report language:
  - Spanish

Request in English:

- export path:
  - `reports/MyProject/ARCHITECTURE-GRAPHS.md`
- report language:
  - English

## Reuse In New Agents

When creating new agents or skills:

- reuse this pattern to separate user language from technical structure
- keep the export contract stable
- add prompt signals in more than one language
- do not force the user to invoke the skill by name when the intent can be inferred
