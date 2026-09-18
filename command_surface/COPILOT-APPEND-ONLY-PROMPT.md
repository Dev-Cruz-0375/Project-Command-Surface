# Copilot append-only patch — Command Surface

**How to use on the work Mac:** open `new-tool-workspace` in VS Code → Copilot Chat → paste the **Prompt for Copilot** block below (from the fenced ` ``` ` section). You do **not** need to export or email `main.py`.

## What we learned from your project

- Paths: `new-tool-workspace/static/index.html`, `static/app.js`, `static/styles.css`, `app/main.py`
- Stack: static shell + `/static/styles.css` + `/static/app.js` (v0.36.0)
- Views (Executive, Analytics, Work queue, …) are **in-page** `data-view` buttons — **do not touch those / do not edit app.js view logic**
- You already leave the app via topbar: `href="/command-center"`
- **Append pattern:** add `/command-surface` the same way — new page + topbar control only

---

## Prompt for Copilot (copy everything below this line)

```
APPEND-ONLY change for CSIRT Incidents Tracker (new-tool-workspace). Do NOT rewrite existing dashboard panels, sidebar nav-items, app.js view switching, or Jira logic. Do NOT ask me to paste main.py — read app/main.py in this workspace yourself.

Goal: Add a new standalone page "/command-surface" (label: "Command Surface") that can be opened from the home topbar without overwriting any existing tabs.

1) In app/main.py, find how "/command-center" is registered and mirror that exact pattern for "/command-surface" serving a new HTML template/static file. Do not change the command-center route.

2) In static/index.html topbar ONLY, insert a small experience dropdown to the LEFT of the existing "Command Center" link (before the refresh button). Do not remove brand, environment, command-center-link, or refresh.

Use this markup (adapt class names only if required to match styles.css — prefer reusing .command-center-link spacing):

    <label class="experience-switch" title="Open alternate workspace experience">
      <span class="visually-hidden">Experience</span>
      <select id="experience-switch" aria-label="Open experience">
        <option value="" selected>Current Tracker</option>
        <option value="/command-surface">Command Surface</option>
      </select>
    </label>

Add a tiny script at the bottom of index.html BEFORE the existing app.js script tag (do not modify app.js):

    <script>
      (function () {
        var el = document.getElementById("experience-switch");
        if (!el) return;
        el.addEventListener("change", function () {
          if (el.value) window.location.href = el.value;
        });
      })();
    </script>

Optional minimal CSS in styles.css (append at end of file only — do not restyle existing topbar):

    .experience-switch select {
      appearance: none;
      background: transparent;
      color: inherit;
      border: 1px solid rgba(255,255,255,0.18);
      border-radius: 8px;
      padding: 0.4rem 0.75rem;
      font: inherit;
      font-size: 0.85rem;
      margin-right: 0.5rem;
      cursor: pointer;
    }
    .experience-switch select:hover { border-color: rgba(255,255,255,0.35); }
    .visually-hidden {
      position: absolute; width: 1px; height: 1px; padding: 0; margin: -1px;
      overflow: hidden; clip: rect(0,0,0,0); white-space: nowrap; border: 0;
    }

3) Create the new page file for /command-surface. Mirror wherever command-center's HTML lives (templates/ or static/). Prefer static/command-surface.html if command-center is served from static; otherwise match the existing template path.

For the page body: if I have staged a mock at command-surface/index.html or static/command-surface.html, use that. Otherwise create a minimal standalone placeholder with Back to Tracker. Requirements for that page:
- Standalone document (own <html>) — not injected into the SPA shell
- Include a top link/button: href="/" labeled "← Back to Tracker"
- Do not import or replace /static/app.js view logic
- Mock data is fine for v1

4) Bump cache query only if you normally bump versions: styles/app ?v= — optional; skip if unsure.

5) Show me the diff summary: list every file touched. Confirm zero deletions of existing view panels.
```

---

## Exact `index.html` topbar edit (human reference)

**Find:**
```html
    <a class="command-center-link" href="/command-center" title="Return to Information Security Command Center">
      <span aria-hidden="true">◎</span> Command Center
    </a>
    <button class="icon-button" id="refresh" type="button" title="Refresh workspace" aria-label="Refresh workspace">↻</button>
```

**Replace with (append dropdown only — keep both existing controls):**
```html
    <label class="experience-switch" title="Open alternate workspace experience">
      <span class="visually-hidden">Experience</span>
      <select id="experience-switch" aria-label="Open experience">
        <option value="" selected>Current Tracker</option>
        <option value="/command-surface">Command Surface</option>
      </select>
    </label>
    <a class="command-center-link" href="/command-center" title="Return to Information Security Command Center">
      <span aria-hidden="true">◎</span> Command Center
    </a>
    <button class="icon-button" id="refresh" type="button" title="Refresh workspace" aria-label="Refresh workspace">↻</button>
```

**Find near end:**
```html
  <script src="/static/app.js?v=0.36.0"></script>
```

**Replace with:**
```html
  <script>
    (function () {
      var el = document.getElementById("experience-switch");
      if (!el) return;
      el.addEventListener("change", function () {
        if (el.value) window.location.href = el.value;
      });
    })();
  </script>
  <script src="/static/app.js?v=0.36.0"></script>
```

---

## Files to copy onto the Mac before / while Copilot runs

1. Copy this session’s mock → project as e.g. `command-surface/index.html`  
   (from personal staging: `csirt-incident-tracker-mock/index.html`)
2. Tell Copilot: “Use `command-surface/index.html` as the body for the `/command-surface` route; add Back to Tracker → `/`.”

---

## Also paste for Copilot (if route discovery fails)

Tell it to search the repo for `command-center` and clone that pattern:

```
rg -n "command-center" .
```

Whatever serves that path is what `/command-surface` should mirror.
