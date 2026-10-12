# Landscape: AI coding usage in a Linux bar

Date: 2026-10-11. Method: read the code (`Panel.qml`, `Main.qml`, `Agent.qml`, `manifest.json`) and one web search. Only search-returned facts are cited; no page was fetched in depth.

## Who else does this

| Project | What it is | Source |
|---|---|---|
| CodexBar | macOS menu-bar app: session and weekly limits for Codex, Claude and others, plus a `codexbar` CLI and cost report | https://github.com/steipete/CodexBar (forks: https://github.com/sibbl/CodexBar), install via https://formulae.brew.sh/cask/codexbar |
| ClaudeBar | macOS menu-bar app for Claude, Codex, Antigravity and Gemini quotas | https://github.com/kiminmonaco/ClaudeBar (fork with Copilot and Kiro: https://github.com/tddworks/ClaudeBar) |
| ccusage | CLI that parses Claude Code's local JSONL to report usage; not official | https://github.com/ryoppippi/ccusage |
| xbar recipe for Claude Code usage | pipes ccusage JSON into xbar on macOS | https://preslav.me/2025/08/04/put-claude-code-token-usage-macos-toolbar/ |

All the polished peers are macOS. The search found no Linux or Quickshell equivalent, which is this plugin's niche.

## What this repo does differently

- Native Omarchy bar panel with theme colours, not a text export.
- Pure renderer: it reads usage records that `omarchy-agent-usage-update` writes to `~/.local/state/omarchy/agents/usage/`, so it never needs credentials itself.
- Pace-aware limit meters, prepaid balance and ledger, tokens by day and by model, optional cross-device sync through a shared folder.

## What users expect, and gaps

1. Clear positioning. `AGENTS.md` records that the bar currently shows usage from Omarchy's stock `akitaonrails.ai-usagebar`, not this widget. A user installing it from the README cannot tell that.
2. A real screenshot. `preview.png` is a bar crop with no panel in it.
3. Threshold notifications (open roadmap item). Peers lead with "how much is left", and alerts are the natural next step.
4. Provider enable/disable through `omarchy settings`: provider defaults live in `manifest.json`, but there is no settings schema (open roadmap item).

## Repo-state findings

- `ROADMAP.md` lists "Color theming using `Color.muted` / `Color.urgent`" as future work; `Panel.qml` already uses both. Stale item, ticked in the new roadmap.
- `Main.qml` (945 lines) embeds a bash scan script in a QML string; editing it breaks the umbrella's tests. Hard to maintain; see simplification in the plan.
- The repo is a published subtree of `duketopceo/omarchy-plugins`; direct commits are overwritten by `scripts/publish.sh` (roadmap U2).
