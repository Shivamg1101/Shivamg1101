# Sales Manager Portal

Live multi-branch sales dashboard with counsellor-level drill-down.

> **Private repository.** This page describes the system at a product and architecture
> level. No configuration, credentials, connection details, schema or business figures
> are included.

## Context

Sales numbers lived in a set of per-branch spreadsheets maintained by different people in
different shapes. Answering "how is this branch doing today, and who is behind" meant
opening several files and reconciling them by hand.

## What it does

- Live dashboard across every branch, drilling down to individual counsellor performance
- Daily revenue derived from month-to-date snapshots, so a single day can be isolated
  even though the upstream sheets only ever report a running total
- Escalation routing with role-based assignment
- Walk-in tracking, matched against admissions to flag conversions
- Student onboarding views per branch
- Google Business Profile reviews, with replies sent from inside the portal

## Architecture notes

The interesting problem here is **ingesting input you don't control**. The upstream sheets
arrive in two different shapes — one groups rows under a branch header, the other carries
an explicit branch column — and both are edited by hand, daily, by different people.

The parser is built around that reality:

- **Branch sections are identified by shape rather than by position**, and reconciled
  against the header row, so the layout can change without the numbers moving with it.
- **Tab matching is whitespace-tolerant**, since a hand-typed name is not a reliable key.
- **A failed read is reported as a failure**, never as an empty result — so absence is
  always distinguishable from a genuine zero.

That last property is the one that matters most. When a data pipeline reads from a source
humans edit, the dangerous failure isn't the one that crashes — it's the one that quietly
returns nothing and looks exactly like a real result.

Counting is per person, not per row — a repeat visitor is one conversion, however many
times they appear.

## Stack

React · Node.js / Express · PostgreSQL · Google Sheets API · OAuth 2.0

Caching uses stale-while-revalidate with conditional HTTP, so the dashboard stays
responsive without hammering the upstream sheets.

---

[← back to profile](https://github.com/Shivamg1101)
