# Okta API token: prod secrets checklist

Checked: 2026-11-24 (read-only scan of portal-ng). Hashes and values intentionally not recorded.
`[x]` = on the new token. `[ ]` = still on the old token.
Skipped: alerts-service-secrets (per owner).
Out of scope for now: reporter-poc-all-properties, usermanagement-poc-all-properties (per owner).
Consumers read the value at startup: restart them after a change (CronJobs pick it up on next run).

## Secrets
- [x] activity-log-service-okta-secret / OKTA_API_KEY
  - Deployments: activity-log-service, activity-log-service-canary
- [x] usermanagement-secret / OKTA_API_KEY
  - Deployments: usermanagement
- [ ] reporter-okta-secret / OKTA_API_KEY
  - Deployments: reporter-canary (first), reporter, gms-ng-db
- [ ] usermanagement-secret / okta.api.key (stale)
  - Consumers: none
- [ ] reporter-secret / okta.api.key (stale)
  - Consumers: none

## ConfigMaps (literal old token)
- [ ] gms-all-properties (connectivity.properties:8)
  - Deployments: gms
- [ ] gms-canary-all-properties (connectivity.properties:8)
  - Deployments: gms-canary
- [ ] okta-account-utils-properties (application.properties:5)
  - CronJobs: okta-account-utils (every 20 min)
- [ ] user-revocation-utils-properties (application.properties:5)
  - CronJobs: user-revocation-utils (every 20 min)

## Open
- [ ] health-monitor-secret / okta.api.key holds an unrecognized token (was empty): confirm owner
- [ ] Revoke old token, only after all boxes above are checked and Okta System Log shows no old-token calls
