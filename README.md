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

## Notes

This is intentionally a panel-only plugin. It does not write usage records; it only visualizes the ones already on disk. With no enabled agents the widget hides itself from the bar.

## License

MIT
