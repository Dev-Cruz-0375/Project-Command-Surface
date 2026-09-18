# Handoff: Personal Cursor (iPad) → Work MacBook → Existing CSIRT App

## Goal
Append a **new sub-page** to the existing localhost **CSIRT Incident Tracker** without overwriting current tabs/layouts. Home page gets a corner dropdown → open the new experience (working name: **Command Surface** / `WOW FACTOR BUILD`).

## What to take from this cloud session

| File | Purpose |
|------|---------|
| `csirt-incident-tracker-mock/index.html` | Full showstopper UI (Brief / Queue / Correlations / Integrations) |
| `csirt-incident-tracker-mock/WOW-FACTOR.md` | Research + pattern map for stakeholders |
| `csirt-incident-tracker-mock/README.md` | How to run / what to try |

Also copy any screenshots/video from the agent artifacts if you want design reference on the Mac.

**Do not** paste work Jira API tokens, corp SSO cookies, or internal ticket PII into the personal Cursor account. Keep this lane as **UI + IA mock**; wire secrets only on the work Mac with approved tooling.

---

## Step 1 — Get files onto the work MacBook (pick one)

Cursor on the iPad won’t sync code into your corp Mac by itself. Export, then import:

1. **Zip download from this agent run** (cursor.com/agents → this chat → download / copy files if available), AirDrop or USB to Mac  
2. **Personal GitHub/GitLab private repo** (no company secrets): push mock folder from a machine that can access the agent files, clone on Mac into a staging folder  
3. **iCloud / OneDrive / email zip** to yourself  

On the Mac, put a staging copy somewhere safe first, e.g. `~/Desktop/csirt-command-surface-staging/`.

---

## Step 2 — Find how the existing app serves pages

On the work Mac, in the **CSIRT Incident Tracker** project (VS Code + Copilot), identify the stack:

| If you see… | You’re probably on… | New page means… |
|-------------|----------------------|-----------------|
| `index.html`, multiple `.html` files, static server | Static / vanilla | Add `command-surface.html` (or a folder) + link from home |
| Vite/React/Next `src/pages` or `app/` | SPA / Next | Add a **route** e.g. `/command-surface` + nav dropdown |
| Express/FastAPI serving `public/` | Backend + static | Drop HTML/JS into `public/command-surface/` + route if needed |

**Rule:** treat the existing Brief / Queue / Global SOC tabs as frozen. Only **add** files and a small nav hook on the home shell.

---

## Step 3 — Append-only integration (recommended layout)

```text
CSIRT-Incident-Tracker/          ← existing project root
├── index.html                   ← home (existing) — ADD dropdown only
├── ... existing tabs/assets ... ← untouched
└── command-surface/             ← NEW folder (append-only)
    ├── index.html               ← paste/adapt our mock
    ├── wow-factor.md            ← optional docs
    └── assets/                  ← if you split CSS/JS later
```

Working name options for the dropdown label:
- **Command Surface** (recommended — product-sounding)
- **Attack Narrative**
- **WOW Factor Build** (fine for internal/dev)

Dropdown value / path: `#/command-surface` or `/command-surface/` or `command-surface/index.html`.

---

## Step 4 — Home page dropdown (minimal, non-destructive)

Add a control in the **top-right of the existing home chrome** (doesn’t replace sidebar tabs):

```html
<!-- Add near existing header actions — do not remove current nav -->
<label class="view-switch" style="margin-left:auto">
  <span class="sr-only">Open experience</span>
  <select id="experienceSwitch" aria-label="Open experience">
    <option value="">Current Tracker</option>
    <option value="command-surface/">Command Surface</option>
  </select>
</label>
<script>
  document.getElementById('experienceSwitch')?.addEventListener('change', (e) => {
    const v = e.target.value;
    if (v) window.location.href = v; // or router.push(v) in React
  });
</script>
```

For React/Vue: same idea — one `<select>` or menu in the app shell that `navigate('/command-surface')` without deleting old routes.

**Back link:** on the Command Surface page, add “← Back to Tracker” → `/` or `index.html` so operators aren’t trapped.

---

## Step 5 — Wire later (on work Mac only)

Keep phase 1 as **static UI with mock data** so you don’t block on approvals.

Phase 2 (corp Mac + approved Copilot/harness):
1. Point ingest at existing Jira CSIRT client already in the project (reuse, don’t duplicate)
2. Stream Copilot/harness events into the agent panel (SSE/WebSocket)
3. Map ontology fields → attack-path nodes / blast BFS
4. Leave old tabs as the “classic” layouts for comparison

---

## Step 6 — Workflow going forward (iPad plan → Mac build)

| Where | Use for |
|-------|---------|
| **Personal iPad + Cursor** | Planning, mocks, IA, HTML experiments (no corp secrets) |
| **Work Mac + VS Code Copilot** | Real project edits, Jira API, ontology, commit to corp repo |
| **Handoff artifact** | Zip or private personal git of `command-surface/` + this checklist |

Optional: after each planning session, drop an updated `command-surface/index.html` into staging and merge on Mac with Copilot (“append this folder; add dropdown on home; do not modify existing dashboard routes”).

---

## Checklist before you call it done

- [ ] Existing tabs still load unchanged  
- [ ] Dropdown on home opens Command Surface  
- [ ] Command Surface has “Back to Tracker”  
- [ ] No overwrite of old widget HTML/JS  
- [ ] No secrets in personal Cursor / personal git  
- [ ] Corp repo commit message notes “append-only command-surface”
