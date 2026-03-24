# /psmux — Agent Teams Split Panes for Claude Code

A Claude Code slash command that installs and toggles [psmux](https://github.com/psmux/psmux) (Windows terminal multiplexer) for Agent Teams split-pane mode.

## What it does

1. **Checks/installs psmux** — if not installed, installs via `winget`
2. **Enables Agent Teams** — sets `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` in settings.json if not already enabled
3. **Toggles on/off** — turn split-pane agent teams on or off

## Usage

```
/psmux        # toggle on/off
/psmux on     # enable
/psmux off    # disable
```

## Installation

Copy `psmux.md` to your Claude Code commands directory:

```bash
cp psmux.md ~/.claude/commands/psmux.md
```

Then restart Claude Code. The `/psmux` command will be available.

## Requirements

- Windows 11
- Claude Code v2.1.32+
- `winget` (for auto-installing psmux)

## How it works

When enabled, run `psmux` in your terminal, then launch `claude` inside the psmux session. When you create an agent team, each teammate spawns in its own split pane automatically.
