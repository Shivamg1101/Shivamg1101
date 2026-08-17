# AI & Automation Suite

Production automation across SkillCircle's operations — built and owned end to end.

> **Internal work.** There is no public repository. This page describes the system at
> a product and architecture level; no configuration, credentials, endpoints or
> customer data are included.

## Context

Operations ran on manual routine: onboarding students by hand, chasing fee payments,
issuing certificates one at a time, and reviewing sales performance in a daily meeting.
Each of these was reliable only while someone remembered to do it.

## What it does

**49 workflows built, 8 running in production** on daily and real-time schedules.

- **Sales performance alerting** — joins counsellor rosters, walk-in logs and live
  telephony data, computes role-specific call targets (counsellor, team lead and
  telecounsellor are held to different bars, adjusted for walk-in load), and escalates
  below-target agents to their manager automatically. This replaced the daily review.
- **RAG support agent** — retrieves from the brochure corpus and drafts responses to
  inbound queries from the retrieved source material rather than free-generating.
- **LMS student lifecycle** — daily onboarding provisioning plus scheduled archive and
  unarchive, removing standing manual work from student operations.
- **Certificate generation and delivery** in real time, plus fee reminders and weekly
  feedback collection.
- **Ad-creative pipeline** that extracts competitor ad structure and generates campaign
  variants for marketing.
- **Browser extension with a webhook receiver** capturing and deduplicating notification
  data into a ~10,000-record store.

## Architecture notes

Workflows are event- and schedule-driven rather than one monolith, so a failure in one
lane doesn't stop the others. Anything touching money or student records is idempotent —
reruns are safe, which matters when a scheduled job retries.

The reporting workflows deliberately read from the systems of record rather than keeping
their own copy, so there is no second source of truth to drift.

## Stack

n8n · OpenAI · RAG · Pabbly Connect · AiSensy · Chrome extension · webhooks

Integrated against six systems: LMS, CRM, billing, telephony, business profile and
transactional email.

---

[← back to profile](https://github.com/Shivamg1101)
