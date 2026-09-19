# My Agents

A personal fork of the stock `omarchy.agents` widget for Omarchy, extended with extra provider support and custom display tweaks.

## Install

```bash
omarchy plugin add https://github.com/duketopceo/omarchy-agents
omarchy plugin enable lukedaduke.agents
```

## What it shows

One bar icon and one panel for every AI coding subscription the machine reports. The panel is a read-only display: it watches usage records that `omarchy-agent-usage-update` writes to `~/.local/state/omarchy/agents/usage/` and renders whatever appears there.

- Hero row with provider, plan, and spend status
- Subscription switch when more than one agent is enabled
- Limit meter and reset timer
- Prepaid balance and credit ledger
- Tokens by day and tokens by model, with tooltips

## Requirements

This plugin is a renderer only — it ships no collectors. It needs:

- `omarchy-agent-usage-update` at `~/.local/bin/` (ships with Omarchy). The panel checks for it and shows a "setup required" state if it is missing.
- `omarchy-launch-tui` / `omarchy-agent` for the launch and login buttons (optional; display works without them).

## Sync (optional)

Set `syncMode` to `On` and point `syncDir` at a folder shared between machines (Syncthing, Dropbox, rsync). Each machine writes a snapshot named after `syncDeviceId`/`syncFileName` (default `<hostname>.json`) and merges the snapshots it finds. Snapshots over 1 MiB, symlinks, and non-regular files are skipped. `syncDeviceId` overrides the device name stored inside the aggregate.

## Remove

```bash
omarchy plugin remove lukedaduke.agents
```

## Notes

This is intentionally a panel-only plugin. It does not write usage records; it only visualizes the ones already on disk. With no enabled agents the widget hides itself from the bar (unless the update helper is missing — see Requirements).

## License

MIT
