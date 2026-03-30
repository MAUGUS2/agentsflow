<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/MAUGUS2/agentsflow/main/assets/agentsflow-banner.svg" />
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/MAUGUS2/agentsflow/main/assets/agentsflow-banner.svg" />
    <img src="https://raw.githubusercontent.com/MAUGUS2/agentsflow/main/assets/agentsflow-banner.svg" alt="AgentsFlow" width="720" />
  </picture>
</p>

<h1 align="center">AgentsFlow</h1>

<p align="center">
  <strong>Agents flowing between your tools.</strong><br/>
  The universal AI agent manager for the multi-platform era.
</p>

<p align="center">
  <a href="https://github.com/MAUGUS2/agentsflow/blob/main/LICENSE"><img src="https://img.shields.io/github/license/MAUGUS2/agentsflow?style=flat-square&color=a855f7" alt="License" /></a>
  <a href="https://github.com/MAUGUS2/agentsflow/stargazers"><img src="https://img.shields.io/github/stars/MAUGUS2/agentsflow?style=flat-square&color=a855f7" alt="Stars" /></a>
  <a href="https://fluity.ai"><img src="https://img.shields.io/badge/by-Fluity_Agents-7c3aed?style=flat-square" alt="Fluity Agents" /></a>
  <a href="https://github.com/MAUGUS2/skillflow"><img src="https://img.shields.io/badge/sister-SkillFlow-00d4aa?style=flat-square" alt="SkillFlow" /></a>
</p>

<p align="center">
  <a href="#what-is-agentsflow">What is it</a> &bull;
  <a href="#what-problem-does-agentsflow-solve">The problem</a> &bull;
  <a href="#what-agents-does-agentsflow-support">Supported agents</a> &bull;
  <a href="#how-does-agentsflow-work">How it works</a> &bull;
  <a href="#packages">Packages</a> &bull;
  <a href="#roadmap">Roadmap</a>
</p>

---

## What is AgentsFlow?

AgentsFlow is a unified platform to **discover, orchestrate, monitor, and manage AI coding agents** across every tool and environment you use — from a single control plane.

Today, developers use 3-5 AI coding agents simultaneously: Claude Code for complex reasoning, Codex for quick edits, Cursor for IDE workflows, Copilot for autocomplete, Antigravity for Google integrations. Each agent has its own configuration, capabilities, and context window — but **no tool manages the agents themselves**.

> **The problem:** You have Claude Code, Codex, Cursor, Copilot, and Antigravity installed. Each has different configs, different context limits, different strengths. You manually decide which agent to use for each task. There's no way to see what agents are available, what they can do, or how they're performing.
>
> **The solution:** AgentsFlow provides a unified registry of all your AI agents, their capabilities, health status, and performance. It routes tasks to the best agent, shares context across agents, and gives you one dashboard to manage everything.

## What problem does AgentsFlow solve?

The AI agent landscape in 2026 is **fragmented by design**. Each vendor builds their agent as a silo:

```
┌──────────────────────────────────────────────────────────────┐
│                    Your development environment              │
│                                                              │
│  🟣 Claude Code    → ~/.claude/         (Anthropic)          │
│  🟢 Codex CLI      → ~/.codex/          (OpenAI)             │
│  🔵 Antigravity    → ~/.gemini/         (Google)             │
│  ⬛ Cursor          → ~/.cursor/         (Anysphere)         │
│  🌊 Windsurf       → ~/.codeium/        (Codeium)           │
│  🐙 GitHub Copilot → .github/           (Microsoft)         │
│  🔶 Warp AI        → ~/.warp/           (Warp)              │
│                                                              │
│  ❌ No unified view                                          │
│  ❌ No cross-agent orchestration                             │
│  ❌ No shared context or memory                              │
│  ❌ No performance monitoring                                │
│  ❌ Manual agent selection for every task                    │
└──────────────────────────────────────────────────────────────┘
```

AgentsFlow sits **above** all your agents, providing the management layer that no vendor will build (because each wants to be your only agent).

## What agents does AgentsFlow support?

| Agent | Vendor | Config Directory | Status |
|-------|--------|-----------------|--------|
| **Claude Code** | Anthropic | `~/.claude/` | Supported |
| **Cowork** | Anthropic | Via plugins | Supported |
| **Codex CLI** | OpenAI | `~/.codex/` | Supported |
| **Google Antigravity** | Google | `~/.gemini/` | Supported |
| **Cursor** | Anysphere | `~/.cursor/` | Supported |
| **Windsurf** | Codeium | `~/.codeium/` | Supported |
| **GitHub Copilot** | Microsoft | `.github/` | Supported |
| **Warp AI** | Warp | `~/.warp/` | Planned |
| **Amp** | Sourcegraph | `~/.amp/` | Planned |
| **OpenHands** | All Hands AI | `.openhands/` | Planned |
| **Goose** | Block | `~/.goose/` | Planned |

## How does AgentsFlow work?

AgentsFlow operates in four layers:

```
┌──────────────────────────────────────────────────────┐
│                  @agentsflow/dashboard                │
│         React UI · Agent cards · Performance          │
├──────────────────────────────────────────────────────┤
│                   @agentsflow/mcp                     │
│      MCP Server · Cross-agent orchestration           │
├──────────────────────────────────────────────────────┤
│                   @agentsflow/cli                     │
│       Interactive terminal · Low-token interface       │
├──────────────────────────────────────────────────────┤
│                   @agentsflow/core                    │
│  Discovery · Registry · Health · Routing · Context    │
└──────────────────────────────────────────────────────┘
```

### Core capabilities

- **Agent Discovery** — Automatically detect all installed AI agents, their versions, and configurations
- **Unified Registry** — One place to see every agent, its capabilities, health, and current status
- **Task Routing** — Route tasks to the best agent based on type, complexity, and agent strengths
- **Context Sharing** — Share relevant context between agents without duplicating tokens
- **Health Monitoring** — Track agent availability, response times, and error rates
- **Config Management** — Manage agent configurations from one place, sync settings across environments

## Quick start

```bash
# Install globally
npm install -g agentsflow

# Discover all installed agents
agentsflow scan

# See agent status and health
agentsflow status

# List capabilities per agent
agentsflow agents --detail

# Route a task to the best agent
agentsflow route "refactor this module" --context ./src

# Launch the management dashboard
agentsflow dashboard
```

### As an MCP server

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "agentsflow": {
      "command": "npx",
      "args": ["-y", "@agentsflow/mcp"]
    }
  }
}
```

## Packages

| Package | Description | Status |
|---------|-------------|--------|
| [`@agentsflow/core`](https://www.npmjs.com/package/@agentsflow/core) | Engine — discovery, registry, health, routing | Planned |
| [`@agentsflow/cli`](https://www.npmjs.com/package/@agentsflow/cli) | Interactive terminal interface | Planned |
| [`@agentsflow/mcp`](https://www.npmjs.com/package/@agentsflow/mcp) | MCP server for cross-agent orchestration | Planned |
| [`@agentsflow/sdk`](https://www.npmjs.com/package/@agentsflow/sdk) | SDK for building agent integrations | Planned |
| [`@agentsflow/agents`](https://www.npmjs.com/package/@agentsflow/agents) | Agent registry and definitions | Planned |
| [`@agentsflow/registry`](https://www.npmjs.com/package/@agentsflow/registry) | Public agent catalog | Planned |

## How is AgentsFlow different?

AgentsFlow is the **management layer** that sits above individual agents. It's not another AI agent — it's the tool that manages all of them.

| Concern | Individual Agents | AgentsFlow |
|---------|------------------|------------|
| Scope | One vendor's agent | All agents unified |
| Config | Per-agent, scattered | Centralized, synced |
| Visibility | What this agent sees | What ALL agents see |
| Selection | Manual, per-task | Automated routing |
| Health | Per-agent logs | Unified monitoring |
| Skills | Per-agent directories | Synced via [SkillFlow](https://github.com/MAUGUS2/skillflow) |

## How does AgentsFlow relate to SkillFlow?

AgentsFlow and [SkillFlow](https://github.com/MAUGUS2/skillflow) are **sister projects** in the Fluity ecosystem:

- **[SkillFlow](https://github.com/MAUGUS2/skillflow)** manages **skills** (what agents know how to do)
- **AgentsFlow** manages **agents** (the AI systems themselves)

Together, they provide complete visibility and control over your multi-agent development environment. SkillFlow ensures skills flow between agents; AgentsFlow ensures agents flow between your tools.

## Architecture decisions

AgentsFlow is built on the same principles as SkillFlow:

1. **CLI-first, MCP-optional** — Agents excel at terminal commands. `agentsflow status` costs ~200 tokens vs. 44,000+ for a full MCP schema. MCP is available for structured enterprise workflows.

2. **Agent-agnostic** — AgentsFlow doesn't favor any vendor. It treats every agent as a first-class citizen with a standardized interface.

3. **Progressive disclosure** — Only essential metadata loads at startup. Detailed agent capabilities, health data, and configuration load on demand.

4. **Complementary, not competitive** — AgentsFlow doesn't replace your agents. It makes them work better together by providing the orchestration layer that no single vendor will build.

## Tech stack

`TypeScript` · `MCP SDK` · `Zod` · `Commander.js` · `React` · `Vite` · `pnpm workspaces`

## Roadmap

- [x] Reserve npm packages (`@agentsflow/*`) and GitHub repo
- [ ] **v0.1** — Core engine: agent discovery, registry, health checks
- [ ] **v0.2** — CLI: `agentsflow scan`, `status`, `agents`, `config`
- [ ] **v0.3** — MCP server: cross-agent tools with progressive disclosure
- [ ] **v0.4** — Task routing: automatic agent selection based on task type
- [ ] **v0.5** — Dashboard: React UI with agent cards and health monitoring
- [ ] **v0.6** — Context sharing: bridge context between agents
- [ ] **v1.0** — Stable release with full orchestration and monitoring

## Contributing

AgentsFlow is open source and welcomes contributions. The project uses pnpm workspaces with a `packages/` + `apps/` monorepo structure.

```bash
git clone https://github.com/MAUGUS2/agentsflow.git
cd agentsflow
pnpm install
pnpm dev
```

## License

[MIT](LICENSE) — use it, fork it, make it better.

---

<p align="center">
  <sub>Built with care by <a href="https://fluity.ai"><strong>Fluity Agents</strong></a></sub>
  <br/>
  <sub>Part of the Fluity ecosystem — <a href="https://github.com/MAUGUS2/skillflow">SkillFlow</a> · AgentsFlow · more coming soon</sub>
</p>