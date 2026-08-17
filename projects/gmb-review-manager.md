# GMB Review Manager

Live Google Business Profile review monitoring and reply, across every branch, from one
console.

> **Private repository.** Product and architecture level only — no configuration,
> credentials, account or location identifiers.

## Context

Each branch has its own Google Business Profile listing. Reviews were monitored ad hoc,
which meant they were monitored inconsistently — and an unanswered review is visible to
every future customer looking at that branch.

## What it does

- Pulls reviews across all locations into a single console
- Replies are sent from the portal, so responding doesn't require access to the
  underlying business account
- Monitoring runs on a schedule rather than on someone remembering to look

## Architecture notes

The notable constraint was authentication. The Business Profile API does **not** accept
service-account credentials for this use case, so the integration runs a full three-legged
OAuth flow with refresh-token handling and renewal — the account has to be genuinely
delegated, not impersonated.

That single fact drove the design: because tokens expire and can be revoked, the system
treats loss of authorisation as an expected state with a defined recovery path, rather
than as a crash.

Scheduled polling is used rather than webhooks, since the review feed offers no push
mechanism.

## Stack

Node.js / Express · Google Business Profile API · OAuth 2.0 · PostgreSQL · node-cron

---

[← back to profile](https://github.com/Shivamg1101)
