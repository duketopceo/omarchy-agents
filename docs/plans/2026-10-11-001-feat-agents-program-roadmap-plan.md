---
title: "Program roadmap: omarchy-agents (My Agents)"
type: feat
status: active
date: 2026-10-11
---

# Program roadmap: omarchy-agents

Written directly (not via `ce-plan`): small plugin repo, and the roadmap is mostly decisions rather than build work. All required fields are present.

## Scope and constraints

- Plugin id `lukedaduke.agents`; `Panel.qml` (about 1,090 lines), `Main.qml` (about 945), `Agent.qml`, seven provider SVGs.
- Subtree of `omarchy-plugins`: land changes there first (U2).
- Umbrella tests extract and run the bash script inside `Main.qml`; do not touch its escaping without running them.
- QML cannot be run outside Omarchy.

## Units

### Now

**U1. Decide: publish, or keep personal.** Status: open (first item of the existing checklist). Evidence: `ROADMAP.md` says no public differentiator; `AGENTS.md` says the bar shows stock `ai-usagebar` instead. Verification: a one-line decision recorded in `ROADMAP.md`.
- Difficulty: easy (a decision).
- Feasibility: none technical; depends on the owner.
- Simpler alternative: mark the repo "personal fork, not for marketplace" and drop the launch checklist; deletes five open items.

**U2. Land this PR in the umbrella.** Status: open. Evidence: `AGENTS.md` provenance. Verification: `scripts/publish.sh agents` fast-forwards with this PR's files.
- Difficulty: medium (docs/brand files are not in the umbrella subtree today).
- Feasibility: umbrella branch protection and `publish.sh` non-fast-forward handling.
- Simpler alternative: move `DESIGN.md`, `docs/`, `assets/brand/` into the umbrella plugin directory.

**U3. Real `preview.png` of the panel.** Status: open. Evidence: current image is a bar crop with no panel. Verification: image shows hero row, meters and model table.
- Difficulty: easy.
- Feasibility: needs the owner's live session (no reload by agents).
- Simpler alternative: drop the image until captured.

**U4. UI pass (done in this PR).** Setup-required state uses the urgent colour. Difficulty easy; QML untestable here.

### Next

**U5. Enable the widget in the bar in place of stock `ai-usagebar`.** Status: open. Evidence: `AGENTS.md` runtime contract. Verification: bar shows this widget's data. 
- Difficulty: easy to medium: bar config change plus checking parity of what the bar label shows.
- Feasibility: owner's bar layout; two widgets reading the same records could double-trigger updates.
- Simpler alternative: leave stock `ai-usagebar` in the bar and use this plugin only for the panel.

**U6. Settings schema for providers.** Status: open. Evidence: `manifest.json` `defaults.providers` exists, no schema. Verification: toggling a provider in `omarchy settings` hides it.
- Difficulty: medium.
- Feasibility: depends on the Omarchy settings-schema shape for nested maps.
- Simpler alternative: document editing the defaults; nothing to build.

**U7. Threshold notifications.** Status: open. Verification: crossing 80 percent once fires one notification, not one per refresh.
- Difficulty: hard (state to avoid repeats, notification path from a plugin).
- Feasibility: needs a notification API the shell exposes to plugins; unconfirmed.
- Simpler alternative: colour the bar label urgent over a threshold.

### Later

**U8. Cross-device aggregation UI.** Difficulty: medium; the sync scan exists, the UI does not. Feasibility: a shared folder is a user-run Syncthing or similar. Simpler alternative: a one-line "from N devices" label.

**U9. More providers.** Difficulty: easy per provider if `omarchy-agent-usage-update` already writes the record (the panel is generic); hard if it must collect new data (this repo ships no collectors). Simpler alternative: contribute collectors upstream and add only an SVG here.

## Simplifications found

- `Main.qml` embeds a bash script as a QML string (`startSyncScan`); move it to `bin/` and read it with a `Process`, which makes it lintable (`shellcheck`) and removes escaping hazards. Needs the umbrella test extractor updated, so not trivial.
- `ROADMAP.md` "Color theming" item is already done: delete.
- `Panel.qml` at about 1,090 lines holds hero, switch, meters, ledger and model rows as inline components; splitting into `components/` files would shrink the main file, at the cost of the host's relative-import rules (unverified).

## Verification

From the umbrella: `python3 scripts/validate-manifests.py`; `python3 -m pytest tests/test_agents.py -q` (Linux). Standalone: `python3 -m json.tool manifest.json`.
