# AGENTS.md — My Agents (`lukedaduke.agents`)

> This file is the agent entry point for this repo.
> Full agent context lives at: https://github.com/duketopceo/luke-agents

Inherits from [luke-agents/AGENTS.md](https://github.com/duketopceo/luke-agents/blob/main/AGENTS.md). This file specializes; it does not replace.

## What This Repo Does

A personal fork of the stock `omarchy.agents` widget, extended with extra
provider support and display tweaks. Shows per-agent coding-token usage in the
bar with a dropdown of providers.

## Provenance — edit in the umbrella, not here

This repo is the published subtree of
[`duketopceo/omarchy-plugins`](https://github.com/duketopceo/omarchy-plugins) at
`plugins/lukedaduke.agents/`. `scripts/publish.sh` runs `git subtree split` and
fast-forwards this repo's `main`. **A commit made directly here is deleted on the
next publish.** Make the change in the umbrella, then `scripts/publish.sh agents`.

## Layout

| Path | Role |
|---|---|
| `manifest.json` | Plugin contract. `kinds: ["bar-widget"]` |
| `Main.qml` | Widget logic. Contains the embedded `startSyncScan()` bash script |
| `Agent.qml` | Per-agent row component |
| `Panel.qml` | Bar text + dropdown |
| `assets/` | Per-provider SVG glyphs (`claude`, `codex`, `cursor`, `devin`, `factory`, `fireworks`, `openrouter`) |
| `ROADMAP.md` | Planned work |
| `preview.png` | Marketplace listing image |

**There is no `bin/` and no Python in this repo.** The scan is a bash script
embedded as a `var script` string inside `Main.qml`, invoked as
`bash -c <script> $0=<dir>`.

## Runtime Contract

- **No build step.** Nothing to compile. `manifest.json` must stay valid JSON.
- **QML cannot be checked outside Omarchy.** The QML imports `Quickshell`,
  `Quickshell.Io`, `QtQuick.Controls`, `qs.Commons`, and `qs.Ui`. The `qs.*`
  modules come from the host shell at runtime, so `qmllint` reports unresolvable
  imports in a plain checkout. Not a bug.
- `moduleName` and `ipcTarget` must both equal the manifest `id`
  (`lukedaduke.agents`).
- The bar currently shows usage from Omarchy's stock
  `akitaonrails.ai-usagebar`, **not** from this widget. That is a known state,
  not a bug to fix here — the umbrella `AGENTS.md` records it.
- A missing `omarchy-agent-usage-update` must render as an explicit
  "setup required" state, not an empty bar.

## Validation

There is no test suite in this repo, but the umbrella covers this plugin's scan
logic in `tests/test_agents.py`, which **extracts the bash script out of
`Main.qml` and executes it**. Editing that string — including whitespace or
escaping — breaks the tests. From the umbrella:

```bash
python3 scripts/validate-manifests.py
python3 -m pytest tests/test_agents.py -q
```

**`tests/test_agents.py` requires Linux.** The embedded script ends in a GNU
`head -z` pipeline; BSD `head` on macOS rejects `-z`, so all 8 tests in that file
fail locally with `head: invalid option -- z` while CI is green. Do not
"fix" the script for macOS and do not report these as regressions.

Real verification is on Linux with the plugin enabled: providers appear, the
dropdown lists them, and the launch/login buttons work when the optional CLIs
exist.

## Runtime Requirements

- `omarchy-agent-usage-update` at `~/.local/bin/` — ships with Omarchy. The panel
  checks for it and shows "setup required" when absent
- `omarchy-launch-tui` / `omarchy-agent` — optional, for the launch and login
  buttons. Display works without them
- Linux with GNU coreutils (`head -z`)

## Conventions

- Theme with `qs.Commons` `Color` / `Style` only. No hardcoded palette hex.
- When editing the embedded `startSyncScan()` script, keep the QML string
  escaping valid and re-run `tests/test_agents.py` — it is the only guard.
- The script must stay bounded (file count and per-file size caps). The tests
  assert those caps.
- Never edit `/usr/share/omarchy/`.
- Bump `version` in `manifest.json` when shipping a behavior change.
