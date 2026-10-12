# Design direction: Gauge

Status: proposal. Method: the `refero-design` research-first method (reference lock, decision ledger, anti-slop gate). The Refero MCP was not available in this session; references are the Omarchy shell kit and the macOS peers named in the landscape note (CodexBar, ClaudeBar), which were not re-fetched.

## 1. Direction

**Name: Gauge.** The panel is an instrument cluster: one hero row, then horizontal meters. A meter is the only graphic. Everything is the user's Omarchy theme: foreground, muted, urgent, accent.

Memorable detail: the model table draws its share bar behind the row label (already in `ModelRow`), so the whole dashboard stays on one screen with no chart library.

## 2. Reference lock

```text
Primary direction: the Omarchy shell kit (Color, Style, Button, PanelToolTip).
Preserve: theme colours only; Style.cornerRadius; Style.font.* sizes; bar font family.
Borrow only: "how much is left" as the first thing on screen (CodexBar, ClaudeBar).
Role rules: urgent = a fault (setup missing, limit near) only; muted = secondary text;
  accent = selected provider.
Reject: hardcoded hex, pie charts, animated gradients, emoji, provider brand colours in chrome.
```

## 3. Decision ledger

| Decision | Role | Why |
|---|---|---|
| Colours from `Color.*`, `Style.selectedFillFor` | theme owns palette | follows any Omarchy theme |
| Meters are flat bars, `radius = height/2` track | the one graphic | readable at a glance, no chart dependency |
| Setup-required text uses `urgent` (this PR) | state | a missing helper is a fault, not an empty list |
| Provider SVGs in `assets/` are content, not chrome | icons | real marks, with a text-glyph fallback already coded |
| Share bars at 0.05 / 0.14 foreground alpha | table | tinting without a second hue |

## 4. Tokens

None of its own; mapping: text `bar.foreground`, secondary `Color.muted`, fault `Color.urgent`, ground `Color.popups.background`, selection `Style.selectedFillFor(foreground, Color.accent)`. Type: `Style.font.display` (hero mark), `title`, `body`, `bodySmall`, `caption`. Contrast of text on ground is the theme's; I did not compute ratios across themes. Static brand colours and their ratios: `assets/brand/README.md`.

## 5. Icon style

Provider marks are per-vendor SVGs; the plugin falls back to the bar glyph when one fails to load. Brand mark: three horizontal meters in a rounded square, 64 px grid, square-cornered bars.

## 6. Motion

One animation: the model share bar width, 160 ms OutCubic. Nothing loops. Keep it that way.

## 7. Surfaces

| Surface | File |
|---|---|
| Bar icon / label | `Main.qml` / `Panel.qml` bar part |
| Panel: hero, provider switch, limit meters, ledger, model table | `Panel.qml` |
| Per-agent record reader | `Agent.qml` |
| README, listing image | `README.md`, `preview.png` (roadmap U3) |

## 8. Anti-slop gate

No default indigo, no glass, no gradients, no decorative icons: pass. One graphic type (meter), reused: pass.
