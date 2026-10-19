<!-- TNDS-HEADER:BEGIN -->
<div align="center">
  <h1>Parallel Agent Framework</h1>
  <h3>Runs two or three AI agents on one codebase with declared file zones and a shared log, so they stop overwriting each other.</h3>
  <img src="https://raw.githubusercontent.com/Jjohnston70/Jjohnston70/main/true-north-logo-layered-v3.png" alt="True North Data Strategies" width="240" />
  <br /><br />
  <a href="#stack"><img src="https://img.shields.io/badge/Built%20with-PowerShell%20%7C%20Shell-0A8EA0?style=for-the-badge" alt="Built with PowerShell | Shell" /></a>
  <a href="https://truenorthstrategyops.com"><img src="https://img.shields.io/badge/Built%20by-TNDS-1F6FEB?style=for-the-badge" alt="Built by TNDS" /></a>
  <a href="#contact"><img src="https://img.shields.io/badge/Contact-TNDS-181717?style=for-the-badge" alt="Contact" /></a>
</div>
<!-- TNDS-HEADER:END -->

## What this is

A provider-agnostic coordination framework for running two or three AI agents (Claude, ChatGPT, Ollama, or any LLM) on the same project at the same time. Each agent owns a track, works in its declared file zones, and coordinates through a shared log. It ends merge conflicts between agents, duplicated work and silent assumptions.

It is markdown templates, two init scripts and a protocol. No runtime, no dependencies, no lock-in.

![Parallel Agent Framework](Parallel-AgentStack.png)

_The Parallel Agent Framework mark._

| Part | What it does |
|---|---|
| Track | Assigns each agent a track (frontend, backend, devops) with declared file zones |
| Coordination log | The single source of truth for task status, blockers and API contracts |
| Task completion protocol | Every finished task produces a completion record, the next prompt and a log update |
| Integration checkpoints | Points where agents stop and verify their work connects |
| Templates | Three instruction templates and a one-page reference card, listed below |

## Quick start

```bash
git clone https://github.com/Jjohnston70/parallel-agentstack.git
cd parallel-agentstack
```

Windows (PowerShell):

```powershell
.\tools\init-project.ps1 -ProjectPath "C:\Users\you\Desktop\my-project"
```

Mac or Linux:

```bash
chmod +x tools/init-project.sh
./tools/init-project.sh ~/Desktop/my-project
```

The script creates `AI-INSTRUCTIONS.md`, `AGENT_COORDINATION_LOG.md`, and starter prompts for each agent. Paste `AI-INSTRUCTIONS.md` into each agent chat window, hand each agent its starter prompt, and go.

To start from a different template, pass its file name as the second argument to `init-project.sh`, or as `-Template` to `init-project.ps1`.

| Guide | What it covers |
|---|---|
| [docs/QUICKSTART.md](docs/QUICKSTART.md) | Full setup walkthrough |
| [docs/README-AI-PARALLEL-DEVELOPMENT.md](docs/README-AI-PARALLEL-DEVELOPMENT.md) | Framework deep-dive |

Every guide lives in [docs/](docs/).

## How it works

```
  Agent A (Frontend)           Agent B (Backend)           Agent C (DevOps, optional)
        |                            |                              |
        |-- src/components/          |-- src/api/                   |-- .github/
        |-- src/pages/               |-- src/server/                |-- tests/
        |-- src/styles/              |-- src/db/                    |-- docker/
        |                            |                              |
        +---------> AGENT_COORDINATION_LOG.md (shared) <-------------+
                         |
                         v
              Integration Checkpoint
              (stop, verify, document, continue)
```

## Templates

| File | What it is | Use when |
|---|---|---|
| `AI-PROJECT-TEMPLATE-PROMPT.md` | 2-agent with file zones, the default | A standard two-track build |
| `AI-PROJECT-TEMPLATE-3AGENT.md` | 3-agent: Frontend, Backend and DevOps | You need a third agent for DevOps or testing |
| `AI-AGENT-NO-FILE-RULES-PROMPT.md` | Coordination only, no file rules | An existing project where file zones would get in the way |
| `AI-AGENT-REFERENCE-CARD.md` | One-page cheat sheet | Keeping the protocol in front of you while you work |

## Project structure

```
.
├── templates/
│   ├── AI-PROJECT-TEMPLATE-PROMPT.md        # 2-agent with file zones (default)
│   ├── AI-PROJECT-TEMPLATE-3AGENT.md        # 3-agent (Frontend / Backend / DevOps)
│   ├── AI-AGENT-NO-FILE-RULES-PROMPT.md     # Coordination-only, no file rules
│   └── AI-AGENT-REFERENCE-CARD.md           # One-page cheat sheet
├── examples/
│   └── AI-AGENT-EXAMPLE-SAAS-DASHBOARD.md   # Worked example
├── docs/
│   ├── QUICKSTART.md
│   └── README-AI-PARALLEL-DEVELOPMENT.md
└── tools/
    ├── init-project.ps1                     # Windows scaffolding
    └── init-project.sh                      # Mac/Linux scaffolding
```

## Core principles

| Principle | What it means in practice |
|---|---|
| No silent assumptions | If an agent needs something, it writes it in the log |
| Structured handoffs | Every completed task produces a completion record, next prompt and log update |
| File zone ownership | Each agent has declared zones to prevent conflicts |
| Integration checkpoints | Periodic stops to verify the tracks connect |
| Provider-agnostic | Works with any LLM that can follow instructions |

## Rules for changes

| Rule | What it means |
|---|---|
| No runtime dependencies | No Node or Python package. It stays a text-and-scripts framework. |
| Pure init scripts | No network calls, no secrets, no writes outside the target project path |
| Self-contained templates | Templates are copied verbatim into user projects, so they carry no cross-file references |
| No provider or project type baked in | Templates work with any LLM and any stack, from Next.js to Django, Go or mobile |

## License

MIT, see [LICENSE](LICENSE).

## Stack

| Layer | Tools |
|---|---|
| Templates and guides | Markdown |
| Init scripts | PowerShell, Bash |
| Runtime | None |

<!-- TNDS-FOOTER:BEGIN -->
## Contact

Jacob Johnston | True North Data Strategies LLC, SDVOSB | Colorado Springs, Colorado

jacob@truenorthstrategyops.com | [truenorthstrategyops.com](https://truenorthstrategyops.com) | [pipelinepunks.com](https://pipelinepunks.com)

_Maintained by the TNDS README steward. Last reviewed 2026-10-19._
<!-- TNDS-FOOTER:END -->
