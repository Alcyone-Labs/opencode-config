# OpenCode Config

Personal agent configurations for development workflows.

## Agents

### enhancer

Refines raw prompts before they reach other agents. Investigates context, resolves ambiguities, produces structured outputs with phases and tasks. Use when prompts are vague or lack necessary context. Inspired by AugmentCode's "Enhance Prompt".

### architect

Designs scalable architectures and maintains technical docs/PRDs. NEVER writes code. Outputs markdown documentation with diagrams, trade-offs, and implementation notes. Best for: architectural decisions, system design, PRD refinement.

### lint-fixer

Fixes lint errors by modifying actual code. NEVER adds eslint-disable comments or changes config. Runs `pnpm lint:check`, fixes errors, repeats until clean. Use for: cleaning up lint debt before commits. Inspired by https://github.com/otrebu/agents/tree/main/plugins/development-lifecycle/skills/fix-eslint.

### brainstorming

Subagent that generates creative feature ideas and optimizations. Grounded in existing architecture. Outputs structured proposals with pros/cons for stakeholder review. Best for: exploring alternatives before committing to design.

### skill-forge

Creates [Agent Skills](https://agentskills.io/) following official guidelines. Handles research, structure validation, and packaging. Produces ZIP-ready folders with Skill.md. Use for: building reusable, shareable agent workflows. Strongly inspired by the structure of https://github.com/dmmulroy/cloudflare-skill/.

## Usage

Each agent lives in `~/.config/opencode/agent/` folder (or locally in your project under `./.opencode/agent`). Invoke via OpenCode or compatible platform by loading the respective skill/agent definition.

Agents are opinionated and follow specific workflows—read individual configs for detailed behavior.
