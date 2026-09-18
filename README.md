# Project Command Surface

Planning and UI pack for the **CSIRT Incidents Tracker** Command Surface experience.

## Layout

```text
command_surface/
  index.html                 Showstopper UI (Brief / Queue / Correlations / Integrations)
  COPILOT-APPEND-ONLY-PROMPT.md
  MANIFEST.md
  mock/                      Copy-ready HTML for Tracker static/
  docs/                      Research + handoff notes
  prompts/                   Copilot prompts
  stubs/                     Route placeholder + work Tracker index snapshot
  screenshots/               Mock screenshots + demo recordings
```

## Local preview

```bash
cd "command_surface"
python3 -m http.server 8765
```

Open http://127.0.0.1:8765/

## Work Mac Tracker

Append-only route `/command-surface` in the existing Tracker; see `command_surface/docs/HANDOFF-TO-WORK-MAC.md` and the Copilot prompt.
