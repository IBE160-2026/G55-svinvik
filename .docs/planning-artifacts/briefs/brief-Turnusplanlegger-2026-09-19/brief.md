---
title: "Product Brief: Turnusplanlegger"
status: draft
created: 2026-09-19
updated: 2026-09-19
---

# Product Brief: Turnusplanlegger

## Executive Summary

Turnusplanlegger is a web app that helps the manager of a microbiology diagnostics lab turn a weekly attendance list (who works day, evening or is off) into a proposed assignment of people to lab stations. It respects minimum coverage of analyses, each person's competence level and rotation, and it flags every conflict instead of hiding it.

Today the manager does this by hand in Excel. She receives a Word file with the week's attendance, reformats it so her spreadsheet formulas work, and then spends at least a day each week deciding who goes where, holding competence, coverage, wishes and rotation in her head. The reformatting is wasted time; the assignment is where her mental energy goes.

The app is a school project (IBE160) with a real user waiting: it must satisfy the course requirements and be good enough that she can use it. The manager always treats the plan as a proposal she reviews and edits, so the goal is to shift her work from *deciding* to *checking*.

## The Problem

The lab is mainly divided into bacteriology and PCR, each with many sub-stations (e.g. substrate production, fungal lab). Every week the manager must place each present employee at a station so that:

- **Minimum coverage** of each analysis is met every day. This is a hard rule; when someone calls in sick the team steps up, but that is the exception.
- **Competence levels** are respected. Trainees add capacity beyond the minimum but do not count toward it.
- **Rotation** keeps competence from going stale and prevents boredom. It is a soft rule, but the most important of the soft ones.
- Norwegian working-time law and collective agreements are followed.

The plan is a living document: sickness, leave and courses change it during the week, and she usually resolves gaps by asking colleagues in person. Beyond the weekly plan, she also plans vacation wishes and holiday staffing ahead of time. None of these rules is written down; much of it lives in one person's head.

## The Solution

Import the week's attendance, combine it with a register of employees, stations and competence levels, and produce a proposed weekly assignment laid out like today's spreadsheet so colleagues recognise it. Where minimum coverage cannot be met, or rotation had to be postponed to protect coverage, the app says so, and the manager chooses whether to accept a suggested fix or resolve it herself. She then edits freely, sees the effect on coverage immediately, and exports the week to Excel so the department can keep working from a file that looks like today's sheet.

## What Makes This Different

There is no novel-algorithm claim. The value is fit: a tool shaped around this lab's actual sheet, rules and working style, in which the manager stays the decision-maker. Generic scheduling products do not model station-level competence decay or this lab's rules. The honest risk is that the real rules are not yet written down, so capturing them with the manager is part of the project.

## Who This Serves

**Primary: the lab manager.** She sets up the weekly plan, owns all rules, and needs to trust and quickly verify a proposal.

**Secondary: lab employees.** They read the plan (via the shared export) and, in later phases, submit vacation and holiday wishes through a form the manager enters into the app.

## Success Criteria

- **School:** a working web app with a database and good UI/UX that solves a real problem and can actually be used.
- **Manager:** she uses the app for real weekly plans and spends clearly less time than today's day per week. `[ASSUMPTION: e.g. four consecutive weeks; confirm with her]`
- Every proposal shows which constraints were met and which were bent.

## Scope

**Constraints:** one developer who works full time and builds this on the side, so time outside work is the scarce resource and has to be prioritised. The school deadline is in about three months, but development continues after it: the deadline is a milestone, not the end of scope. Stack: HTML/CSS/JavaScript, Python, SQL. The repository is public, so only anonymised data may be committed; real use requires encrypted personal data and privacy compliance.

**Sequencing principle:** nothing below is dropped, only ordered. What is submitted at the deadline must be a coherent, working product on its own, so v1 is built first and later phases follow after submission.

**v1 (in):**
- Register of employees, stations and competence levels (including trainee)
- Weekly attendance input: from the Word file if a workable sample arrives, otherwise manual or CSV entry `[ASSUMPTION]`
- Minimum coverage per station per day
- Proposed weekly assignment with conflict and postponed-rotation warnings
- Manual editing with live coverage feedback
- Record of who worked where and when (feeds rotation and holiday fairness)
- Export of the week to Excel (.xlsx) in the same layout as today's sheet; PDF as a possible secondary option
- Manager-only login

**Later phases** `[ASSUMPTION: order proposed, not confirmed]`**:**
- Phase 2: vacation and holiday wishes with prioritised lists ("where I want off / where I can work if needed"), submitted by employees on a form the manager enters into the app
- Phase 3: holiday staffing proposals (reduced coverage on holidays; fairness from history), built on the wishes and availability collected in phase 2

**Out for now:** generating the shift plan itself (D/A/Fri), employee login, automatic mid-week reassignment, and legal-rule enforcement until the rules are confirmed.

## Risks and Open Questions

- **Word file format:** no sample yet; parsing is the biggest technical unknown. Name matching is a risk (shared first names, varying spellings).
- **Rotation:** rules and the definition of "stale" (weeks away from a station) must come from the manager. They vary with individual wishes and competence-building.
- **Boundary:** does she also adjust the shift plan, or only assign tasks?
- **Legal and agreement rules:** the exact working-time and collective-agreement rules are to be gathered at the meeting.
- **Vacation conflicts:** what is the fairness rule when two people want the same period?
- **Hosting and privacy:** where may the app run for real use, and who may open it?
- **Sharing changes with the department:** a PDF goes stale and invites version confusion when the manager edits the plan. An Excel export is easier to keep working with, but it is still a snapshot; the department only sees edits live if the file sits in a shared location she re-exports to, or if the app offers a read-only view. Which approach is acceptable to the employer is open.
- **Scope versus deadline:** time outside a full-time job is limited and the deadline is about three months away; phases 2 and 3 will likely land after it. The submitted version must not depend on them to feel complete.

## Vision

If it works, the lab gets a living planning tool: weekly assignment in minutes, holiday staffing and vacation wishes handled with visible fairness, and a competence picture that shows where the team is thin before someone calls in sick. Employees eventually submit wishes directly, and the rules the manager carries in her head become explicit and shared.
