# Relics of the Athenaeum — Belayer Edition

A 5-act multi-agent collaborative quest for [Belayer](https://github.com/donovan-yohan/belayer). Six AI characters with distinct personalities, expertise, and **tool restrictions** work together — guided by a Game Runner (Dungeon Master) — to solve computational challenges, recover lost knowledge fragments, and restore an ancient artifact.

> **Credit**: This quest is adapted from the original [Scion Athenaeum](https://github.com/donovan-yohan/scion-athenaeum) by the same author. The challenges, narrative, and character concepts are preserved; the orchestration layer has been rebuilt for Belayer.

---

## What This Demonstrates

- **Personality-driven agents**: Each character has a distinct voice, expertise, and ego. They argue, delegate, and occasionally steal each other's credit.
- **Hard tool boundaries**: A researcher with no code execution *must* ask a coder to run experiments. A scribe with only file tools can only watch and write. These aren't suggestions — they're enforced by Belayer's `enabled_toolsets` system.
- **Emergent collaboration**: The party splits into sub-teams, validates each other's work, broadcasts findings, and sends direct messages. No single agent can do everything.
- **Quality control that actually works**: The validator agent (Thorne) catches real bugs — typos, incorrect shift values, bad regex — and forces corrections before the quest advances.

---

## The Cast

| Character | Role | Toolsets | Personality |
|-----------|------|----------|-------------|
| **Game Runner** | Dungeon Master / Orchestrator | *all* | The voice of the quest. Reveals challenges, evaluates solutions, advances the narrative. |
| **Lyra the Logician** | Algorithms & code | `file`, `code_execution` | Precise, methodical, slightly condescending. Lives for Dijkstra and XOR. |
| **Kael the Chronicler** | Research & information | `web`, `file` | Curious, thorough, humble. Can't run code — must delegate execution. |
| **Mira the Mapper** | Data transformation | `file`, `code_execution`, `terminal` | Visual thinker. Sees structures and patterns. Good at parsing messy formats. |
| **Thorne the Sentinel** | Validation & testing | `file`, `code_execution` | Skeptical, thorough, dry. Nothing passes until proven. |
| **Zara the Weaver** | Integration & orchestration | `file`, `code_execution`, `terminal` | Pragmatic, fast, occasionally oversteps. Keeps the party moving. |
| **The Scribe** | Chronicler & observer | `file` only | Silent observer. Writes the dramatic transcript and structured journal. Never participates. |

**Peripheral characters** (summoned on demand):
- **The Oracle** — Deep domain knowledge
- **The Healer** — Debugging & error recovery
- **Sprites** — Ephemeral workers for sub-tasks

### Agent Identity → Character Mapping

Each character is defined by a directory in `.belayer/agents/<name>/` containing:
- `agent.yaml` — model, toolsets, runtime config
- `system-prompt.md` — personality, voice, and roleplay instructions
- `AGENTS.md` — operational notes (what tools to use, how to behave)

The directory name (`lyra`, `kael`, `mira`, etc.) is the Belayer agent identity. The `system-prompt.md` assigns the fantasy name and personality. This separation lets you swap characters without changing orchestration logic.

---

## Quest Structure

```
Act I: The Shattered Codex     — Party assembles, decodes the Ancient Summons, navigates the Gateway Map
Act II: The Split Realms       — Party divides. Formats vs Patterns. Two realms, two fragments.
Act III: The API Convergence   — REST API reconstruction + broken contract repair
Act IV: The Deep Archive       — Resonant frequency alignment + corrupted regex restoration
Act V: The Final Assembly      — Master key construction, SHA-256, activation code. The Codex is restored.
```

Each act has 1–2 challenges with real computational puzzles (ciphers, graph traversal, API specs, regex, hashing).

---

## Prerequisites

- **Belayer** with the `enabled_toolsets` patch (branch `quest-athenaeum` or PR #104)
- **Hermes Agent** installed (`~/.hermes/hermes-agent`)
- **Model access** — default is `moonshotai/kimi-k2.6` for all agents. Edit `agent.yaml` to change.

---

## Quick Start

### 1. Build Belayer

```bash
cd /path/to/belayer
go build ./cmd/belayer
```

### 2. Start the Daemon

```bash
cd /path/to/belayer-athenaeum
export HERMES_AGENT_PATH=~/.hermes/hermes-agent
export PYTHONPATH="~/.hermes/hermes-agent:$PYTHONPATH"

pkill -f "belayer daemon"  # clean up any old one
sleep 2

./path/to/belayer daemon --workdir . --socket .belayer/daemon.sock
```

### 3. Launch the Quest

```bash
export BELAYER_SOCKET=.belayer/daemon.sock

./path/to/belayer run start \
  --name athenaeum \
  --task "Begin Relics of the Athenaeum. Initialize workspace, spawn all character agents (lyra, kael, mira, thorne, zara, scribe), write game-context.md, broadcast the opening scene, deploy Act I Challenge 1.1, and begin monitoring. The quest playbook is in playbook/. Use workspace/ for all shared files."
```

### 4. Watch the Story Unfold

```bash
# Party roster
BELAYER_SOCKET=.belayer/daemon.sock belayer roster

# Live logs
BELAYER_SOCKET=.belayer/daemon.sock belayer logs <session-id> --follow

# The Scribe's tale (updates in real-time)
tail -f workspace/quest-tale.md

# Structured journal
tail -f workspace/quest-journal.md
```

---

## Runtime

- **Act I**: ~10–15 min
- **Act II**: ~15–20 min (sub-teams run in parallel)
- **Act III**: ~15–20 min
- **Act IV**: ~15–20 min
- **Act V**: ~10–15 min

**Total**: ~60–90 minutes for the full quest.

---

## Customization

### Change the Setting

Edit `.belayer/agents/supervisor/system-prompt.md` and `.belayer/agents/supervisor/agents.md` to change the narrative frame. Swap "Athenaeum" for "Space Station", "Cyberpunk City", "Underwater Library", whatever. The Game Runner's opening broadcast sets the tone for everyone else.

### Change Personalities

Each agent has a `system-prompt.md` in `.belayer/agents/<name>/`. Edit:
- **Voice**: first-person vs third-person, formal vs casual, terse vs verbose
- **Ego**: make Lyra even more condescending, make Kael apologetic, make Thorne a conspiracy theorist
- **Flaws**: give Zara a habit of taking credit, give Mira a fear of illusory edges

The system prompts include a **"Your Tools and Limitations"** section — keep that accurate or the agent will get confused.

### Change the Scribe's Style

The Scribe only has `file` tools, so it can only read and write. Edit `.belayer/agents/scribe/system-prompt.md` to change the narrative style:
- **D&D transcript**: "The Game Runner spoke... Lyra stepped forward..."
- **Security camera log**: timestamped, detached, clinical
- **Noir detective**: cynical, smoking metaphors, everyone is suspicious
- **Shakespearean**: thee/thou, dramatic asides, iambic pentameter (good luck)

### Change Models

Edit `.belayer/agents/<name>/agent.yaml`:

```yaml
model: anthropic/claude-sonnet-4
```

Different models give different voices. A party of mixed vendors is chaotic in the best way.

### Free-for-all Mode

Remove `enabled_toolsets` from all `agent.yaml` files. Everyone gets all tools. Watch how collaboration collapses into one agent doing everything. Useful as a control experiment.

### Hardcore Mode

Give the Scribe **zero tools** (`enabled_toolsets: []`). It can only observe via messages. The transcript becomes fragmented, second-hand, and occasionally wrong — like a real historian.

### Swap Challenges

Replace files in `playbook/act-*/challenge-*/data/` with your own puzzles. Keep the solution files in `playbook/act-*/challenge-*/solutions/` so the Game Runner knows what to validate against.

---

## Example Output

See [`examples/quest-tale.md`](examples/quest-tale.md) for a complete dramatized transcript of a successful run. It covers all five acts from the Scribe's perspective — including character dialogue, atmospheric descriptions, and the full narrative arc of the Codex restoration.

---

## Project Structure

```
.
├── README.md                     # This file
├── .gitignore
├── .belayer/
│   └── agents/                   # Agent definitions (yaml + prompts)
│       ├── supervisor/           # Game Runner / DM
│       ├── lyra/                 # Algorithmic problem solver
│       ├── kael/                 # Researcher (no code execution)
│       ├── mira/                 # Data wrangler
│       ├── thorne/               # Validator
│       ├── zara/                 # Integrator
│       ├── scribe/               # Chronicler (file tools only)
│       ├── oracle/               # Domain expert (summoned)
│       ├── healer/               # Debugger (summoned)
│       └── *-sprite/             # Ephemeral workers
├── playbook/
│   ├── act-1/                    # The Shattered Codex
│   ├── act-2/                    # The Split Realms
│   ├── act-3/                    # The API Convergence
│   ├── act-4/                    # The Deep Archive
│   └── act-5/                    # The Final Assembly
│       └── challenge-*/
│           ├── data/             # Challenge inputs
│           └── solutions/        # Canonical answers (GM reference)
├── .design/                      # Design documents
│   ├── characters.md             # Full character definitions
│   ├── game-mechanics.md         # Rules and orchestration
│   ├── quest-scenario.md         # Complete quest narrative
│   └── ...
└── workspace/                    # Created at runtime
    ├── quest-tale.md             # Dramatic transcript
    ├── quest-journal.md          # Structured event log
    ├── solutions/                # Agent-written solutions
    ├── notes/                    # Research findings
    └── sprites/                  # Validation scripts
```

---

## How Toolset Restriction Works

Each `agent.yaml` can specify `enabled_toolsets`:

```yaml
enabled_toolsets:
  - web
  - file
```

This is enforced at the Hermes level — the agent literally cannot see or invoke tools outside those toolsets. It's not a suggestion in the prompt. It's a hard boundary.

Common toolsets:
- `file` — read_file, write_file, patch, search_files
- `code_execution` — execute_code
- `web` — web_search, web_extract
- `terminal` — terminal

If `enabled_toolsets` is omitted, the agent gets all available tools.

---

## Troubleshooting

### "daemon.sock: connect: no such file or directory"
Daemon isn't running or socket path is wrong. Check `.belayer/daemon.sock` exists.

### One agent is doing everything
Check `enabled_toolsets` is set in each `agent.yaml`. Verify your Belayer binary includes the patch (`git log --oneline -3` in your Belayer worktree).

### Agents aren't spawning
The supervisor needs `belayer_spawn_agent` in its `belayer_tools` list. Check `.belayer/agents/supervisor/agent.yaml`.

### Model errors
All agents default to `moonshotai/kimi-k2.6`. Edit per-agent `agent.yaml` to change.

### Validation keeps failing
Thorne is doing his job. Check his broadcast messages — he reports specific issues. Fix them and he'll re-validate.

---

## Credit

- **Original quest design**: [scion-athenaeum](https://github.com/donovan-yohan/scion-athenaeum)
- **Orchestration layer**: [Belayer](https://github.com/donovan-yohan/belayer)
- **Agent runtime**: [Hermes Agent](https://github.com/NousResearch/hermes-agent)

---

## License

MIT
