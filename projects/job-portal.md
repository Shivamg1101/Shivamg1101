# Job Portal

Three-sided marketplace connecting students, employers and placement coordinators.

> **Private repository.** Product and architecture level only — no configuration,
> credentials, schema or user data.

## Context

Placements were coordinated over email and spreadsheets. Employers had no way to search
candidates, students had no way to track applications, and coordinators had no view of
whether the pipeline was healthy.

## What it does

- **Students** build a profile and apply to roles, tracking application status
- **Employers** post roles and search candidates
- **Coordinators** verify users, record placements and monitor platform health

## Architecture notes

Built as a **monorepo** with a Next.js web app and a NestJS API, sharing types across the
boundary so a change to a contract fails at compile time rather than in production.

Work that shouldn't block a request — sending notifications, processing uploads — runs on
a job queue backed by Redis. This matters most on the employer side, where a single action
can fan out to many candidates.

Deployment is split: the web tier and the API are hosted separately and scale
independently, since their load profiles differ sharply.

I authored the system architecture documentation alongside the implementation.

## Stack

Next.js 14 · NestJS 10 · TypeScript · Supabase · PostgreSQL · BullMQ / Redis · Docker ·
transactional email

---

[← back to profile](https://github.com/Shivamg1101)
