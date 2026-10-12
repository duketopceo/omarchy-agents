# Roadmap

Program roadmap (2026-10-11): [docs/plans/2026-10-11-001-feat-agents-program-roadmap-plan.md](docs/plans/2026-10-11-001-feat-agents-program-roadmap-plan.md). Landscape: [docs/research/2026-10-11-landscape.md](docs/research/2026-10-11-landscape.md).

| Unit | When | Difficulty |
|---|---|---|
| U1 Decide: publish or keep personal | Now | easy |
| U2 Land this PR in the umbrella (`omarchy-plugins`) | Now | medium |
| U3 Real `preview.png` of the panel | Now | easy |
| U4 UI pass (setup-required colour) | Done in this PR | easy |
| U5 Put this widget in the bar instead of stock `ai-usagebar` | Next | easy to medium |
| U6 Settings schema for providers | Next | medium |
| U7 Threshold notifications | Next | hard |
| U8 Cross-device aggregation UI | Later | medium |
| U9 More providers | Later | easy to hard |

"Color theming using Color.muted / Color.urgent" below is already implemented in `Panel.qml`.

Earlier notes follow.

---

# Roadmap

## Current status

Installable and validated, but it is a personal fork of `omarchy.agents` with no clear public differentiator yet. **Not ready for an aggressive marketplace launch** until the extra-provider and display work is documented and tested by other users.

## Launch checklist

- [ ] Decide if this should be published at all, or kept personal
- [ ] If publishing, document the extra providers and how to configure them
- [ ] Add a clean `preview.png` showing the panel
- [ ] Add a settings schema so users can enable providers from `omarchy settings`
- [ ] Submit to https://plugins.omarchy.org/publish.html
- [ ] Set GitHub repo topics and social preview

## Future work

- [ ] Support additional providers beyond Claude / Codex / Fireworks
- [ ] Notifications when usage crosses a threshold
- [ ] Cross-device usage aggregation UI
- [ ] Color theming using `Color.muted` / `Color.urgent`
