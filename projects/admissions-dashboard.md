# Admissions Dashboard

Role-based admission platform with SLA timers, replacing a single Google Form.

> **Private repository.** Product and architecture level only — no configuration,
> credentials, schema or applicant data.

## Context

The entire admission intake ran through one Google Form. There was no verification step,
no approval gate, and no way to see whether a given application was moving or stuck.

## What it does

- Separate flows for student, counsellor and admin, each seeing only what their role needs
- Students self-verify their own details, moving correction effort off the counsellors
- A structured admin approval gate before an application progresses
- SLA timers enforcing the 24-hour, 48-hour and 3-day onboarding rules, so a stalled
  application is visible rather than merely late
- Real-time analytics over the pipeline
- Automated transactional email at each state change

## Architecture notes

The data model went through **30+ SQL migrations**. Most of that churn was in modelling
*state* honestly: an application is not a row that gets edited in place but a sequence of
transitions, each with an actor and a timestamp. That is what makes the SLA timers and
the audit trail possible without a second bookkeeping system.

Access control is enforced at the data layer rather than in the UI, so a role boundary
cannot be bypassed by calling the API directly.

I also authored the full document set — product requirements, architecture, design system
and engineering rules — which is what let the schema stay coherent across that many
migrations.

## Stack

Next.js (App Router) · TypeScript · Supabase · PostgreSQL · React Query · Recharts ·
Framer Motion · Zod

---

[← back to profile](https://github.com/Shivamg1101)
