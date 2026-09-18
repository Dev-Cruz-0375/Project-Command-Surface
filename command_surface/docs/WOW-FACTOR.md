# CSIRT Showstopper Research — Wow-Factor Sources

Curated from current AI agent / SOC / security-graph products (2025–2026). Mapped to what belongs in **CSIRT Incident Tracker**.

## Tier 1 — Must incorporate (executive + IR wow)

| Pattern | Proven by | Why it stops executives cold | CSIRT surface |
|---------|-----------|------------------------------|---------------|
| **Attack-path security graph** (L→R entry → lateral → crown jewel) | [Wiz Security Graph](https://www.aledlie.com/reports/wiz-io-security-explainability-ux/), [Vectra Attack Graphs](https://www.vectra.ai/blog/vectra-ai-platform-visualizes-multi-domain-modern-attacks-with-attack-graphs) | Turns “7 critical tickets” into a story: *how they get to us* | Brief + Correlations |
| **Blast-radius simulator** | [ThreatLens](https://github.com/rudrasingh-007/ThreatLens), Datadog Workload Protection | BFS hop animation shows blast if path is exploited | Correlations |
| **Attack replay scrubber** | Vectra, ThreatLens, SAGE timeline | Press play — kill chain unfolds chronologically | Brief War Room |
| **Live agent reasoning canvas** | [SIFT.Glass](https://github.com/edycutjong/siftglass), [agent-think-map](https://github.com/nimrodfisher/agent-think-map), [Agent Flow](https://github.com/patoles/agent-flow), [tracesage](https://kjgpta.github.io/tracesage/) | Watch Copilot *think* — tools, hypotheses, FP shatter | Correlations / Agent HUD |
| **Toxic combination / path confidence** | Wiz “toxic combo”, SIFT confidence shatter | Low-sev tickets chain into critical — agents self-correct live | Correlations |

## Tier 2 — Command-center presence

| Pattern | Proven by | CSIRT fit |
|---------|-----------|-----------|
| **Global threat arcs / globe** | [AegisView-SOC](https://github.com/CyberCoder-IITM/AegisView-SOC), [CrypticBastion](https://github.com/vignesh2027/CrypticBastion) | Brief hero: geo of CSIRT-linked sightings |
| **MITRE ATT&CK heat matrix** | SAGE recommender matrix, AegisView | Brief strip: tactics touched by open tickets |
| **Agentic dashboard mutations** | [AG-WebGL](https://github.com/eddie-nv/ag-webGL), [Agentic Dashboards MCP/A2A](https://fawadhs.dev/blog/agentic-dashboards-mcp-a2a-analytics) | Copilot can *recompose* Brief widgets on ask |
| **3D agent ops floor** | [Nexus HQ](https://github.com/xbrxr03/nexus-hq), [ATC](https://github.com/209512/atc) | Optional Integrations / Agent Ops mode |
| **Investigation graph + event timeline** | Datadog signals, Contra cyber threat map UX | Queue detail → story mode |

## Tier 3 — Polish / immersion (use sparingly)

- Glass HUD + scanline atmospheres (NexCore) — atmosphere only, not the product
- Keyboard War Room shortcuts (AegisView: `W` war room, `R` AI analysis)
- Achievement / cinematic onboarding — skip for enterprise; keep keyboard legend

## Anti-patterns (look wow, feel fake)

- Pure Matrix rain with no data binding
- Unlabeled neon KPI tiles (your old mock risk)
- Graphs that don’t join to real Jira keys / CVE / assets
- Glow-everything cyberpunk purple (reads as template, not SOC)

## Recommended product thesis

> **Don’t add more cards. Make the Brief a living attack narrative.**  
> Copilot streams reasoning → graph grows → replay proves the story → blast radius answers “so what?” → one click opens the CSIRT tickets that evidence it.

## Implementation stack (when you leave mock mode)

- Graph: React Flow + dagre (Wiz L→R) or vis-network
- Globe: Three.js / globe.gl
- Agent stream: SSE from VS Code Copilot harness / MCP
- Replay: event log with timestamps from Jira + ontology
- Actions: MCP tools to mutate dashboard + open Jira
