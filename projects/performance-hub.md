# Performance Hub

Team performance tracker with live state and per-branch leaderboards.

> **Private repository.** Product and architecture level only — no configuration,
> credentials or individual performance data.

## Context

Team performance was reported after the fact, which made it a review artefact rather than
something anyone could act on during the period being measured.

## What it does

- Live performance state, updating without a refresh
- Per-branch leaderboards
- A single view usable by both the team and their managers

## Architecture notes

Built on a realtime datastore so the leaderboard reflects current state rather than a
periodically regenerated report — the whole point is that it is worth looking at *during*
the day.

Client state is deliberately kept small and centralised. With live updates arriving
continuously, the risk is a UI that re-renders constantly; a single store with narrow
subscriptions keeps updates localised to the components that actually changed.

## Stack

React · Vite · Firebase / Firestore · Zustand · React Router

---

[← back to profile](https://github.com/Shivamg1101)
