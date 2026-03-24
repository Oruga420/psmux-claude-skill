# psmux — Toggle Agent Teams Split Panes

Toggle psmux (terminal multiplexer) for Claude Code Agent Teams. Installs psmux and enables Agent Teams automatically if not already set up.

**Usage:** `/psmux` or `/psmux on` or `/psmux off`

## Step 1: Check if psmux is installed

Run `psmux -V` (or `which psmux`) to check if psmux is already installed.

- **If installed**: report the version and continue.
- **If NOT installed**: install it with `winget install -e --id marlocarlo.psmux --accept-package-agreements --accept-source-agreements` and report that it was installed. Tell the user they need to restart their terminal for the PATH to update.

## Step 2: Ensure Agent Teams is enabled

Read `~/.claude/settings.json` and check if `env.CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` exists.

- **If missing or not `"1"`**: add/set it to `"1"` in the `env` object. Report "Agent Teams was not enabled — enabled it now."
- **If already `"1"`**: do nothing, skip silently.

If there is no `env` object at all, create it with the key.

## Step 3: Determine toggle action

Now handle the on/off toggle for the psmux split-pane mode:

- If `$ARGUMENTS` contains "on": set `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` to `"1"` (should already be from Step 2)
- If `$ARGUMENTS` contains "off": set `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` to `"0"`
- If no argument or just `/psmux`: **toggle** — if currently `"1"` set to `"0"`, if currently `"0"` set to `"1"`

## Step 4: Apply the change

Edit `~/.claude/settings.json` and update ONLY the `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` value in the `env` object. Do NOT modify any other settings.

## Step 5: Report the result

Show a summary:

```
psmux: [installed / just installed]  (version X.X.X)
Agent Teams: [ON / OFF]
```

- **ON**: "Restart your terminal, run `psmux`, then `claude` inside the session. Teammates will appear in split panes."
- **OFF**: "Agent teams will not spawn. Restart your terminal for changes to take effect."

## Important

- Do NOT touch any other field in settings.json
- Do NOT add or remove fields besides `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS`
- If the `env` object doesn't exist, create it
