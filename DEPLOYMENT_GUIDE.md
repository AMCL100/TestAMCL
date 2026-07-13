# AgentAdam v2 — Deployment Guide

> **What's in this package:** all the June fixes that never reached the
> team + Copilot's diagnosis fixes + four layout patterns + the new
> Layouts tab in the extension. Apply in order. Total time ~30 minutes.

---

## What's changed since the team last got updates

### From June pilot testing (none of these reached the team)
- **Colour mapping** — Good=blue #017CBE, Bad=orange #E3850D, Neutral=grey #666666
- **Min/Max contextual** — agent asks if high is good, bad, or neutral
- **Alternative palette** — green/red on request (less accessible)
- **Slicer zone narrowed** — 751px (x:1599→2350), page title gets 1200px
- **Slicer widths** — 1=751, 2=370, 3=243, 4=180
- **Visual subtitles** — rewrite or remove vocabulary placeholders, never leave them
- **Page title rule** — agent asks at session start
- **Report title rule** — agent asks at session start
- **Legend defaults** — top-left, 14px (enforced in checklist)
- **SQL review** — reads from TMDL partitions automatically, no paste needed
- **User-facing language** — "top bar / filter pane / canvas" (Zone A/B/C internal only)

### From Copilot's pilot diagnosis
- **PBIR JSON syntax rules** — projections must be an array, even for single field
- **Theme gap flagging** — flag missing theme coverage rather than per-visual overrides
- **Desktop validation checkpoints** — render checks after model phase and first page

### New — layout patterns
- **3/30/300** (default exploration) — glance/scan/dig cognitive layers
- **Narrative** (storytelling) — Z-pattern reading flow
- **Executive** (one big headline) — hero visual with supporting context
- **Operational** (status board) — scannable, no raw data
- Agent picks per page based on purpose, explains why, dev can override

### New — authority hierarchy
1. Template standards — sacred on FORM (zones, coordinates, colours) — never overruled
2. Developer's content and intent — sacred on WHAT — never overruled
3. Developer's layout preferences — adapted to fit the template's form
4. Agent's layout suggestions — only when dev defers
   - Conflicts → agent flags, proposes adapted version, asks approval

Template wins on the mechanics. Developer wins on the content.
Never silently reshape. Never refuse. Always adapt transparently.

---

## Step 1 — Update SharePoint (2 minutes)

This is the highest-priority step. Without it, the agent runs on the
old rules.

```
1. Open the SharePoint folder in your browser:
   https://iberdrola.sharepoint.com/sites/UK%20Operations/UK%20Operations%20Document%20Library/Reporting/Data%20Visualisation/Agentic%20BI%20-%20AgentAdam

2. Upload sharepoint-file/agentadam.instructions.md
   When prompted "Replace?" → click Replace

3. Wait 1–2 minutes for sync to propagate to team machines

4. Done — every developer's next VS Code session uses the new rules
```

---

## Step 2 — Push the GitHub repo updates (10 minutes)

```
1. Open your local AgentAdam repo in VS Code

2. Replace these folders/files with the versions in repo-files/:
     .github/copilot-instructions.md
     .github/plugin/marketplace.json
     plugins/agentadam/.github/plugin.json
     skills/   (entire folder — all 7 skills updated)
     AgentAdam/  (all standards files updated)
     docs/AgentAdam_PLUGIN_TEAM_GUIDE.md
     docs/AgentAdam_WORKFLOW_COLLAPSIBLE.html
     README.md
     ROADMAP.md

3. Open terminal in the repo root:
     git add -A
     git commit -m "v1.1.3 — June fixes, Copilot diagnosis fixes, layout patterns"
     git push

4. Plugin auto-updates within 24h on team machines
   (Or devs can force: Ctrl+Shift+P → Extensions: Check for Extension Updates)
```

---

## Step 3 — Distribute the new VS Code extension (5 minutes)

The extension is v1.0.3 — adds the Layouts tab, updates Reference tab
with new colours/slicer widths, updates Build tab Will Do list.

```
1. The new VSIX is at vscode-extension/agentadam-1.0.3.vsix

2. Post in Teams:
     "AgentAdam extension updated to v1.0.3.
      Download the new VSIX and install:
      Ctrl+Shift+X → ... → Install from VSIX → select the file.
      New: Layouts tab showing the 4 layout patterns we now support."

3. Devs install over the top — VS Code replaces v1.0.2 automatically
```

---

## Step 4 — Tell the team what changed (5 minutes)

The biggest things they'll notice:

```
At session start
  Agent now asks for the REPORT TITLE (top-right text box)

When building
  Agent picks the layout per page and explains why
  Agent will adapt wireframes to fit the template
  Agent flags conflicts rather than silently reshaping

Colour changes
  Good = blue now (was green)
  Bad = orange now (was red)
  Devs may need to update existing visuals if they want
  the new palette — old reports unaffected unless they ask

SQL review
  Just say "Review the SQL for [table name]" — no paste needed

The Layouts tab
  New in v1.0.3 of the extension — shows the four patterns
  and lets you copy a layout prompt directly
```

---

## Verification — confirm everything's working

After deployment, ask any dev to do this in VS Code:

```
1. Open any folder
2. Open Copilot Chat
3. Ask: "What colour means Bad in our charts?"
   Expected: Orange #E3850D
4. Ask: "What are the slicer widths for 4 slicers?"
   Expected: 180px each
5. Ask: "Where do legends default to?"
   Expected: Top-left, 14px
```

If any of those answer wrong, the SharePoint sync hasn't refreshed
on their machine — Ctrl+Shift+P → Developer: Reload Window fixes it.

---

## What's NOT changing

- Kurt's data-goblin plugins (still bundled in your marketplace)
- VS Code setup steps for new joiners
- The SharePoint folder location
- The install commands (still 5 plugin installs per dev)
- The template files (PBIR/SemanticModel)
- Themes file (PBITheme.json)

---

*v1.1.3 plugin, v1.0.3 extension, instructions file dated 2026-06-17*
*Built on data-goblin by Kurt Buhler.*
