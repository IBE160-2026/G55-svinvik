# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project status

This repository is currently in the **planning phase** — there is no application code yet (no frontend, backend, or database implementation, no package manifest). The only substantive artifact so far is the product brief under `.docs/planning-artifacts/`. Do not assume a build/test/lint toolchain exists; check for one (`package.json`, `requirements.txt`, etc.) before assuming commands from a prior session still apply, and update this file once real code and tooling land.

## What this project is

"Turnusplanlegger" (G55 — Claudine) is a group project for the course IBE160 (Programmering med KI) at Høgskolen i Molde. It will be a web app that helps the manager of a microbiology diagnostics lab turn a weekly attendance list into a proposed assignment of people to lab stations (e.g. bacteriology, PCR, and their sub-stations), respecting minimum coverage per analysis, per-person competence levels, and rotation — and flagging conflicts instead of silently resolving them. Full context (problem, scope, v1 vs. later phases, open questions) lives in `.docs/planning-artifacts/briefs/brief-Turnusplanlegger-2026-09-19/brief.md` and `addendum.md` — read those before starting design or implementation work, rather than re-deriving requirements from scratch.

Mandated stack (course requirement): HTML/CSS/JavaScript frontend, Python backend, SQL database, delivered as a web app.

Key constraints from the brief worth keeping in mind while building:
- The manager always stays the decision-maker: the app proposes, flags conflicts, and lets her accept a suggested fix or resolve it manually — it never silently overrides.
- Minimum coverage per station per day is a hard rule; rotation, vacation wishes, and Norwegian working-time rules are soft/compliance rules layered on top.
- v1 scope is weekly task assignment only (register of employees/stations/competence, attendance input, coverage + conflict warnings, manual editing with live feedback, history for rotation/fairness, Excel export, manager-only login). Vacation-wish intake and holiday-staffing proposals are explicitly later phases — don't pull them into v1 work unless asked.

## Privacy / data handling (critical, repo is public)

- This repo is **public**. Only anonymized data may ever be committed. Real employee names, the real weekly-plan PDF/Word files, and any other real personal data must never be added to the repo — `.gitignore` already excludes `*Ukeplan*.pdf` and `*.docx` for this reason; keep that pattern intact and extend it if new real-data file types show up.
- A real-data file (`1 Seksjon Diagnostikk-Ukeplan.pdf`) already exists untracked in the working directory for reference during planning — it must stay untracked. When creating sample/seed/test data for the app, fabricate or anonymize it.

## Repository layout

- `.docs/planning-artifacts/` — BMAD-generated planning documents (briefs, and later PRD/architecture/epics as the project progresses). `briefs/brief-Turnusplanlegger-2026-09-19/` holds the current brief, a Norwegian-language addendum with rules/details gathered from the user that didn't fit the brief template, and `.memlog.md`, a chronological decision log from the brief-writing conversation — useful for recovering *why* a scope decision was made.
- `_bmad/` — the installed BMAD method framework (v6.12.0, modules `core`, `bmm`, `cis`) that drives the planning/build skills listed below. `_bmad/config.toml` and `_bmad/bmm/config.yaml` are installer-managed (regenerated on install, treat as read-only); durable overrides belong in `_bmad/custom/config.toml` (committed) or `_bmad/custom/config.user.toml` (gitignored, personal).
- `.claude/skills/` — the BMAD skills exposed to Claude Code (agent personas Mary/John/Sally/Winston/Amelia for analyst/PM/UX/architect/dev roles, plus brief/PRD/architecture/epics/sprint-planning/build/review/retrospective workflows). This project is meant to be driven through these skills rather than ad hoc prompting — e.g. use `bmad-prd` to produce the PRD, `bmad-architecture` for architecture decisions, `bmad-create-epics-and-stories` → `bmad-sprint-planning` → `bmad-build` to move from requirements to implementation, and `bmad-code-review`/`bmad-retrospective` afterward.
- `README.md` — minimal course/group identification (course IBE160, group member Kristine Green Svinvik).

## Sesjonslogg

**Logg sesjonen.** Når en oppgave/økt avsluttes — før sluttoppsummeringen — bruk `sesjonslogg`-skillen: den logger Oppgave + Plan + Resultat + åpne punkter per bruker i `.logs/<bruker>/`, fører åpne punkter i `.logs/<bruker>/issues.md` og committer loggfilene (alene, i egen commit) rett etter at de er skrevet.
