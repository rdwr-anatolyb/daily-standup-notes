# Okta API token: prod secrets checklist

Checked: 2026-11-24 (read-only scan of portal-ng). Hashes and values intentionally not recorded.
`[x]` = on the new token. `[ ]` = still on the old token.
Skipped: alerts-service-secrets (per owner).

## Secrets
- [x] activity-log-service-okta-secret / OKTA_API_KEY
- [x] usermanagement-secret / OKTA_API_KEY
- [ ] reporter-okta-secret / OKTA_API_KEY (reporter, reporter-canary, gms-ng-db)
- [ ] usermanagement-secret / okta.api.key (stale, no workload reads it)
- [ ] reporter-secret / okta.api.key (stale, no workload reads it)

## ConfigMaps (literal old token)
- [ ] gms-all-properties (connectivity.properties:8)
- [ ] gms-canary-all-properties (connectivity.properties:8)
- [ ] okta-account-utils-properties (application.properties:5, CronJob)
- [ ] user-revocation-utils-properties (application.properties:5, CronJob)
- [ ] reporter-poc-all-properties (connectivity.properties:79, only if poc in use)
- [ ] usermanagement-poc-all-properties (connectivity.properties:42, only if poc in use)

## Open
- [ ] health-monitor-secret / okta.api.key holds an unrecognized token (was empty): confirm owner
- [ ] Revoke old token, only after all boxes above are checked and Okta System Log shows no old-token calls
