<p align="center">
  <img src="branding/AgentAdam_README_Banner.svg" alt="AgentAdam" width="100%">
</p>

<p align="center">
  <strong>Governed AI Assistant for Power BI Development</strong><br>
  <em>SP Customer Business — COE Data Governance &amp; Visualisation</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-TEST-orange" alt="Status: TEST">
  <img src="https://img.shields.io/badge/owner-Adam_McLean-02892E" alt="Owner: Adam McLean">
  <img src="https://img.shields.io/badge/review-fortnightly-blue" alt="Review: Fortnightly">
  <img src="https://img.shields.io/badge/install-VS_Code_plugin-1a56db" alt="Install: VS Code plugin">
  <img src="https://img.shields.io/badge/built_on-data--goblin-017CBE" alt="Built on: data-goblin">
</p>

---

## What is AgentAdam?

AgentAdam is a governed AI assistant for building Power BI reports at SP Customer Business. Built on top of [Kurt Buhler's data-goblin](https://github.com/data-goblin/power-bi-agentic-development) toolkit, it adds company-specific standards, governance, and template rules so GitHub Copilot understands exactly how to build reports the SP way.

It installs as a **VS Code plugin** — once installed, AgentAdam's standards load automatically every session. No manual setup, no startup commands.

The agent knows:

- Our template, zones, bookmarks, and visual vocabulary
- Our DAX standards and naming conventions
- Our colour palette and typography
- Our governance rules and publishing process
- Our SQL review guidance and incremental refresh patterns
- How to review an existing semantic model for size, speed, and best practice
- How to review a report before it goes to production
- How to produce the technical documentation the Governance Framework expects

---

## The skills

Eleven skills, loaded on demand when the agent recognises the task.

| Skill | Triggered by | What it does |
|---|---|---|
| `template-standards` | Any report build | Zones, colours, fonts, layout patterns, and the full visual formatting specification |
| `dax-standards` | Any measure work | Measure patterns, format strings, conditional formatting for max/min highlighting |
| `sql-review` | "review the SQL for [table]" | Reads the query from the model's partitions, critiques it in plain English |
| `semantic-model` | "review my semantic model" | Read-only health check — structure, size, refresh cost |
| `model-evaluation` | "grade my model" | Grading against best practice |
| `incremental-refresh` | Refresh and partition work | Partitioning and refresh strategy |
| `documentation` | "document this report" | Handover notes and measure catalogues |
| `go-live-readiness` | "run a go live readiness review" | SQL, PII, model and measure performance, grain and date boundedness — produces a prioritised review list |
| `production-documenter` | "document this report for production" | The formal Confluence record — owners, lineage, ERD, table detail, measure catalogue, SQL |
| `pbir-structure` | Reference | How to read and interpret PBIR report definitions |
| `visual-reference` | An attached image | Build a page from a screenshot or wireframe — extract intent, never styling |

Developers work through **VS Code GitHub Copilot Chat** — the standards load automatically, there is nothing to type at the start of a session. All work is governed by the standards in this repo.

---

## How it works

```
AgentAdam standards (this repo)   <- Always win - our governance
        |
Kurt's data-goblin toolkit        <- Power BI technical capability
        |
Copilot general knowledge         <- Fills any remaining gaps
```

When AgentAdam standards conflict with general Power BI practice, **AgentAdam wins**. The agent follows our rules first, Kurt's general guidance second, Copilot's training knowledge third.

The standards are delivered two ways from this one repo:

- **As a plugin** — the `skills/` and `.github/copilot-instructions.md` are packaged so VS Code loads them automatically. This is how the team uses it.
- **As readable docs** — the `AgentAdam/` folder holds the same standards in human-readable form, as the governed source of truth.

---

## Who is this for?

```
Power BI developers       Build reports faster with governance built in
Senior developers         Review and approve patterns at scale
COE governance team       Maintain standards in one auditable place
New starters              Onboard onto our standards from day one
```

---

## Getting started

> **Read this first:** [docs/AgentAdam_PLUGIN_TEAM_GUIDE.md](docs/AgentAdam_PLUGIN_TEAM_GUIDE.md)

The short version:

```
HOW IT WORKS
  AgentAdam's core rules live in a shared SharePoint folder that syncs
  to each developer's machine. VS Code reads from that folder automatically
  in every session — no matter which folder is open.
  The plugin adds specialist skills on top (DAX, SQL review, model evaluation,
  documentation) that load on demand.

ONE TIME (per developer)
  1. Check Git is installed:  git --version
     If missing, get it from git-scm.com or your Software Centre
  2. Install VS Code + GitHub Copilot (Microsoft Store / Extensions)
  3. Enable plugins:  Settings → chat.plugins.enabled → true
  4. Install all five plugins:
       Ctrl+Shift+P → Chat: Install Plugin From Source
       → paste:  U357001_ibe/AgentAdam
                 (just the repo path — no plugin name, no https://)
       → the Extensions sidebar opens with all five listed
       → click Install on EACH one
       → confirm under Extensions → Agent Plugins - Installed

       Only agentadam showing? Only one installed. Repeat and
       click Install on the other four.
  5. Sync the SharePoint folder to your machine:
       https://iberdrola.sharepoint.com/sites/UK%20Operations/
       UK%20Operations%20Document%20Library/Reporting/
       Data%20Visualisation/Agentic%20BI%20-%20AgentAdam
       → click Sync in the browser
  6. Add one VS Code user setting:
       "chat.instructionsFilesLocations": {
         "~/IBERDROLA S.A/UK Operations - Agentic BI - AgentAdam": true
       }

EVERY SESSION
  Open VS Code → open your report folder → talk to Copilot.
  Rules are already loaded. No startup sequence.

UPDATES
  Core rules: SharePoint syncs automatically when Adam updates the file
  Plugin skills: auto-update within 24h via the plugin
```

Full detail and troubleshooting in the [plugin team guide](docs/AgentAdam_PLUGIN_TEAM_GUIDE.md).

---

## What you can ask AgentAdam to do

```
BUILDING
  "Build a sales report for a mixed audience..."
  "Write a measure for year-over-year growth"
  "Highlight the highest and lowest bar on this chart"
  [attach a screenshot] "Make mine like this but in our settings"

REVIEWING
  "Review the SQL for the FactDebt table"
  "Review my semantic model"
  "Run a go live readiness review"

DOCUMENTING
  "Document this report"
  "Document this report for production"
```

The agent always presents a plan and waits for your approval before changing
anything. It **never publishes** — you review in Desktop and publish manually.

---

## Repo structure

```
AgentAdam/
|
|-- README.md                            <- You are here
|-- ROADMAP.md                           Future work (docs only)
|
|-- .github/
|   |-- copilot-instructions.md          Auto-loads core rules every session
|   +-- plugin/marketplace.json          Declares this repo as a marketplace
|
|-- plugins/agentadam/.github/
|   +-- plugin.json                      Plugin manifest
|
|-- skills/                              The 11 plugin skills (load on demand)
|   |-- template-standards/              Zones, colours, formatting spec
|   |-- dax-standards/                   Measures and conditional formatting
|   |-- sql-review/                      Query critique from TMDL partitions
|   |-- semantic-model/                  Read-only model health check
|   |-- model-evaluation/                Grading against best practice
|   |-- incremental-refresh/             Partitioning and refresh strategy
|   |-- documentation/                   Handover notes
|   |-- go-live-readiness/               Pre-production review list
|   |-- production-documenter/           Formal Confluence record
|   |-- pbir-structure/                  Reading PBIR definitions
|   +-- visual-reference/                Build from a screenshot
|
|-- AgentAdam/                           Standards source (human-readable)
|   |-- AgentAdam.md                       Main agent instructions
|   |-- AgentAdam_DAX_STANDARDS.md
|   |-- AgentAdam_SEMANTIC_MODEL_SKILL.md
|   |-- AgentAdam_SQL_REVIEW_SKILL.md
|   |-- AgentAdam_INCREMENTAL_REFRESH_SKILL.md
|   |-- AgentAdam_DOCUMENTATION_SKILL.md
|   |-- AgentAdam_MODEL_EVALUATION_SKILL.md
|   |-- AgentAdam_TEMPLATE_STANDARDS.md
|   |-- AgentAdam_RULES_SUMMARY.md         Human reference of all rules
|   |-- AgentAdam_REPORT_HANDOVER_TEMPLATE.md
|   |-- AgentAdam_WIREFRAME_TEMPLATE.md
|   |-- AgentAdam_ATTRIBUTION.md
|   |-- themes/
|   |   |-- PBITheme.json
|   |   +-- AgentAdamTheme_STANDARDS.md
|   +-- templates/
|       |-- PBI_Corporate_Template.Report/
|       |-- PBI_Corporate_Template.SemanticModel/
|       |-- AgentAdam_TEMPLATE_STANDARDS.md
|       +-- AgentAdam_WIREFRAME_TEMPLATE.md
|
|-- data-goblin/                         Kurt Buhler's toolkit (the engine)
|
|-- docs/                                Human-facing guides
|   |-- AgentAdam_PLUGIN_TEAM_GUIDE.md     Install & use - read first
|   |-- AgentAdam_TEAM_GUIDE.md            Original (pre-plugin) guide
|   |-- AgentAdam_DEVELOPER_WORKFLOW.md
|   |-- AgentAdam_OWNER_DUTIES.md
|   |-- AgentAdam_REPORT_PLANNING_TEMPLATE.md  Optional planning aid
|   +-- AgentAdam_WORKFLOW_COLLAPSIBLE.html    Interactive workflow (Chat/CLI)
|
+-- branding/
    |-- AgentAdam_README_Banner.svg
    |-- AgentAdam_Social_Banner.svg
    +-- AgentAdam_Icon.svg
```

---

## The standards are governed - do not edit locally

The `AgentAdam/` folder and the `skills/` are the company standard.

- They are read by the agent on every session
- Branch protection prevents anyone except the owner pushing changes to `main`
- Your local copy is read-only - if you think a rule should change, raise it
  with Adam McLean
- Updates flow to you automatically (plugin) or via `git pull` (cloned repo)

---

## Quick links

| What you need | Where to look |
|---|---|
| Install and use AgentAdam | [docs/AgentAdam_PLUGIN_TEAM_GUIDE.md](docs/AgentAdam_PLUGIN_TEAM_GUIDE.md) |
| Optional report planning template | [docs/AgentAdam_REPORT_PLANNING_TEMPLATE.md](docs/AgentAdam_REPORT_PLANNING_TEMPLATE.md) |
| Interactive workflow (Chat / CLI toggle) | [docs/AgentAdam_WORKFLOW_COLLAPSIBLE.html](docs/AgentAdam_WORKFLOW_COLLAPSIBLE.html) |
| The full standards reference | [AgentAdam/AgentAdam_RULES_SUMMARY.md](AgentAdam/AgentAdam_RULES_SUMMARY.md) |
| Detailed developer workflow | [docs/AgentAdam_DEVELOPER_WORKFLOW.md](docs/AgentAdam_DEVELOPER_WORKFLOW.md) |
| Owner duties and maintenance | [docs/AgentAdam_OWNER_DUTIES.md](docs/AgentAdam_OWNER_DUTIES.md) |
| Where we're heading next | [ROADMAP.md](ROADMAP.md) |
| Kurt's original toolkit | [data-goblin/](data-goblin/) |

---

## Status

**Current phase:** Pilot testing (6 weeks)
**Owner:** Adam McLean - COE Data Governance & Visualisation
**Review cycle:** Fortnightly

This is a test deployment. Standards and workflows will evolve based on real
usage during the pilot. The plugin install is a VS Code preview feature, so
expect the occasional rough edge - feedback is welcome, raise it with Adam.

---

## Attribution

AgentAdam is built on the [data-goblin/power-bi-agentic-development](https://github.com/data-goblin/power-bi-agentic-development) toolkit by **Kurt Buhler**. Kurt's plugins and skills provide the technical capability for the agent to read and edit Power BI files correctly. AgentAdam adds SP Customer Business-specific standards and governance on top of his work.

Kurt's toolkit is licensed **GPL-3.0**, and he has given explicit permission
for this use. Bundled here for internal use within SP Customer Business only —
not redistributed outside the organisation.

Full attribution and licensing in [AgentAdam/AgentAdam_ATTRIBUTION.md](AgentAdam/AgentAdam_ATTRIBUTION.md).

---

<p align="center">
  <em>Built with care by the COE Data Governance &amp; Visualisation team<br>
  SP Customer Business - 2026</em>
</p>
