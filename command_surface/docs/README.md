# CSIRT Incident Tracker — Showstopper Mock

Interactive command surface (not a card wall). Research notes: [WOW-FACTOR.md](./WOW-FACTOR.md).

## Surfaces

| View | Wow pattern | Inspired by |
|------|-------------|-------------|
| **Brief** | L→R attack-path cinema + replay scrubber + live Copilot agent stream + MITRE heat + blast preview | Wiz, Vectra, SIFT.Glass, agent-think-map |
| **Queue** | Ticket list + chronological attack story timeline | Datadog signals, Vectra |
| **Correlations** | Cluster rail + BFS blast-radius simulator + Jira evidence | ThreatLens, Wiz toxic combos |
| **Integrations** | Where Jira / Copilot SSE / ontology / MCP mutations plug in | Agentic dashboards |

## Run

```bash
cd csirt-incident-tracker-mock
python3 -m http.server 8765
```

Open http://127.0.0.1:8765/

### Try

- **Brief → Replay path** or press ▶ on the scrubber
- **War Room** toggles elevated critical-path mode
- Watch the **Copilot agent stream** (FP shatter animation)
- **Correlations → Simulate blast** for hop-by-hop compromise spread
- **Queue** — click tickets to swap the story timeline

Mock data only — not wired to Jira yet.
