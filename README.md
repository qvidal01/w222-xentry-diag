# W222 XENTRY Diagnostics — 2016 S550 AC Repair

Personal reference repo for diagnosing the AC on my own 2016 Mercedes-Benz S550
(W222) with a standalone XENTRY laptop. Clone this onto the diagnostic laptop so
Claude Code there has everything local.

## Contents

| File | What it is |
|------|-----------|
| `docs/LAPTOP-SETUP.md` | Prep checklist for the XENTRY laptop: keeping it from phoning home, and how to run Claude Code alongside XENTRY |
| `docs/xentry-navigation.md` | How to navigate XENTRY: quick test, KLA (climate) control unit, actual values, actuations |
| `docs/w222-ac-diagnosis.md` | W222-specific AC failure modes, decision tree, live-data targets, forum case studies |
| `docs/NOTEBOOK-GAP.md` | What the NotebookLM "xentry" notebook already covers vs. what this repo adds |
| `sessions/` | One dated markdown note per diagnostic session — fault codes pulled, live data readings, actions taken |

## Workflow on the laptop

1. Open XENTRY, connect to the car (ignition on, battery charger connected).
2. Open Claude Code in a terminal in this repo.
3. Run the quick test; screenshot anything unclear (`Win+Shift+S`, save into `sessions/screenshots/`).
4. Ask Claude Code to read the screenshot and the docs here, interpret codes/values, and suggest the next menu/actuation.
5. Log findings into a new `sessions/YYYY-MM-DD.md` as you go.

## Scope

Owner self-diagnosis of my own vehicle only. Reading codes, live data, and
component actuations — no SCN coding, no module programming, nothing that
requires the Mercedes backend.
