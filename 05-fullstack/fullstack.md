# Full-Stack: Data, Access Rules, Edge Cases, Deploy

> Module 5 · Full-Stack. Add data schemas, access rules, and edge cases; stress-test and deploy.

## Deployed link

_The working, shareable link that survives real users._

https://pixel-perfect-copy-3814.lovable.app

## Data schema

| Entity | Key fields | Notes |
|---|---|---|
| user_roles | id, user_id → auth.users, role, UNIQUE(user_id, role) | _____ |
| _____ | _____ | _____ |

## Access rules

_Who can see / do what? Where are the auth boundaries?_

Every new table gets GRANTs before RLS (authenticated + service_role; no anon anywhere).
Role checks only through private.has_role — never client storage.
Accepting an invite runs a server function: verify token, not expired, signed-in email matches invites.email, then insert membership and set accepted in one transaction.
Admin pill and dashboard hidden unless has_role(pm_admin); the database enforces it regardless

## Edge cases hardened

| Case | Before | After |
|---|---|---|
| Empty / first-run state | offline - no indication | offline with indication and retry |
| Bad / malicious input | _____ | _____ |
| Failure / offline | _____ | _____ |

## Stress test results

_What you threw at it, and what held / broke._

All good
