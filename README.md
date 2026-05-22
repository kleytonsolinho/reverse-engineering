# Reverse Engineering

Reverse Engineering is a Codex plugin for deep repository investigation. It packages the reverse-engineering agent as reusable skills that trace real runtime entrypoints, follow execution flows with evidence, map architectural boundaries, and export the result as documentation artifacts.

## Quickstart

Give Codex Reverse Engineering: [Codex App](#codex-app), [Repo Marketplace](#repo-marketplace), [Personal Marketplace](#personal-marketplace).

## How it works

It starts when you ask Codex to understand how a repository actually works.

Instead of answering with a loose summary, the plugin pushes Codex into an investigation workflow:

- read the repository before concluding
- locate bootstrap files and real runtime entrypoints
- trace flows end to end with local evidence
- separate confirmed behavior from hypotheses
- export the findings into `reports/<ProjectName>/`

The workflow is exposed through two complementary skills:

- `reverse-engineering`
  - broad natural-language entrypoint for full repository reverse engineering
- `codebase-reverse-engineering`
  - deeper evidence-driven investigation contract with explicit export requirements

Because the plugin is meant to trigger from natural requests, the goal is not just to answer in chat. A complete reverse-engineering request should end with generated artifacts.

## Installation

Installation is Codex-specific. The important detail is that copying the plugin to disk is not enough by itself. The plugin must also be installed from the Codex plugin UI so it becomes available in-session.

### Codex App

If you already have a marketplace where this plugin appears:

1. Open **Plugins** in the Codex app.
2. Open the marketplace where `Reverse Engineering` is listed.
3. Install the plugin from the UI.
4. Restart Codex if needed.

### Repo Marketplace

Use this when you want the plugin available from one repository.

1. Copy the plugin into the repository:

   ```bash
   mkdir -p ./plugins
   cp -R /absolute/path/to/reverse-engineering ./plugins/reverse-engineering
   ```

2. Add or update `$REPO_ROOT/.agents/plugins/marketplace.json`:

   ```json
   {
     "name": "local-repo",
     "interface": {
       "displayName": "Local Repo Plugins"
     },
     "plugins": [
       {
         "name": "reverse-engineering",
         "source": {
           "source": "local",
           "path": "./plugins/reverse-engineering"
         },
         "policy": {
           "installation": "AVAILABLE",
           "authentication": "ON_INSTALL"
         },
         "category": "Coding"
       }
     ]
   }
   ```

3. Restart Codex.
4. Open the plugin directory in Codex.
5. Select the repo marketplace.
6. Install `Reverse Engineering` from the UI.

### Personal Marketplace

Use this when you want the plugin available across your own Codex projects.

1. Copy the plugin into your personal Codex plugin directory:

   ```bash
   mkdir -p ~/.codex/plugins
   cp -R ./plugins/reverse-engineering ~/.codex/plugins/reverse-engineering
   ```

2. Add or update `~/.agents/plugins/marketplace.json`:

   ```json
   {
     "name": "personal",
     "interface": {
       "displayName": "Personal"
     },
     "plugins": [
       {
         "name": "reverse-engineering",
         "source": {
           "source": "local",
           "path": "./.codex/plugins/reverse-engineering"
         },
         "policy": {
           "installation": "AVAILABLE",
           "authentication": "ON_INSTALL"
         },
         "category": "Coding"
       }
     ]
   }
   ```

3. Restart Codex.
4. Open the plugin directory in Codex.
5. Select the personal marketplace.
6. Install `Reverse Engineering` from the UI.

## The Basic Workflow

1. **reverse-engineering** - Activates on broad reverse-engineering requests in natural language and routes Codex into the plugin workflow.

2. **codebase-reverse-engineering** - Performs the deep repository investigation: entrypoints, boundaries, contracts, runtime flow, and architectural evidence.

3. **report export** - Writes the result into:
   - `reports/<ProjectName>/REVERSE-ENGINEERING.md`
   - `reports/<ProjectName>/ONBOARDING-GUIDE.md`
   - `reports/<ProjectName>/ARCHITECTURE-GRAPHS.md`

4. **artifact-based answer** - The user-facing answer should be grounded in the exported artifacts, not a detached summary.

## What's Inside

### Skills Library

**Investigation**
- **reverse-engineering** - natural-language entrypoint for full repository reverse engineering
- **codebase-reverse-engineering** - evidence-driven codebase investigation with report export contract

**Shared references**
- **multilingual-export-pattern** - shared guidance for keeping file structure fixed while writing report content in the user's language
- **investigation-checklist** - checklist for runtime discovery and evidence gathering
- **output-contract** - required shape of exported reports

### Root plugin instructions

- `AGENTS.md`
  - root behavior for Codex when the user asks for reverse engineering
- `CLAUDE.md`
  - compatibility copy of the same root behavior
- `agents/openai.yaml`
  - root-level plugin metadata for Codex surfaces

## Multilingual behavior

This plugin is prepared to accept requests in natural language, including Portuguese, English, and Spanish.

Rules:

- the user should not need to know the skill name
- the plugin should infer reverse-engineering intent from the request
- the generated reports should be written in the same language as the user's input
- exported file names remain fixed:
  - `REVERSE-ENGINEERING.md`
  - `ONBOARDING-GUIDE.md`
  - `ARCHITECTURE-GRAPHS.md`

## Visual Identity

The plugin currently uses:

- `assets/app-icon.png`

That image is wired in the manifest as:

- `interface.composerIcon`
- `interface.logo`

## Philosophy

- **Evidence over assumptions** - read the repository before concluding
- **Runtime over surface description** - trace what actually happens
- **Exportable understanding** - convert investigation into reusable reports
- **Language flexibility with structural consistency** - adapt report language to the user while preserving stable output paths

## Contributing

When you change this plugin, keep the following aligned:

1. root plugin behavior in `AGENTS.md` and `CLAUDE.md`
2. skill behavior in `skills/reverse-engineering/` and `skills/codebase-reverse-engineering/`
3. manifest metadata in `.codex-plugin/plugin.json`
4. installation instructions in this README

When changing behavior, test at least:

- plugin discovery in the Codex UI
- manual installation from the plugin UI
- skill availability in session
- natural-language triggering
- creation of `reports/<ProjectName>/`

## License

MIT License.
