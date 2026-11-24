# Okta API token rotation (prod): status

Updated: 2026-11-24. Token values and hashes are intentionally not recorded here.

## Done
- activity-log-service secret: new token set, main deployment restarted, startup normal.
- usermanagement secret (`OKTA_API_KEY`): new token set, create/delete verified.
- Read-only prod cluster scan finished.

## Still on the old token
- reporter secret (reporter-canary, reporter, gms-ng-db)
- stale dotted `okta.api.key` entries in usermanagement and reporter secrets
- GMS ConfigMaps, okta-account-utils and user-revocation-utils CronJobs (git change + restart)
- alerts-service holds a non-prod token: replace or remove

## Next steps
1. Restart activity-log-service-canary and verify (test event -> activity-log row).
2. Update reporter secret: canary, reporter, gms-ng-db. Verify new rows keep tenant (reporter returns 200 on bad key).
3. Update GMS ConfigMaps, then the two CronJobs; run one manual job each.
4. Settle stale `okta.api.key` entries and the alerts-service key after a code check.
5. Revoke the old token last, after Okta System Log shows no calls under it for the quiet period (irreversible).

## Gaps
- Rollback point (Vault version) for activity-log-service not recorded.
- Code check pending for ip-groups, geo-blocking, health-monitor key need.
- Scan does not cover Vault, git, or other namespaces.
- Rollback and go/no-go criteria still open.
