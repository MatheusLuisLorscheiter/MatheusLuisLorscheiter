# Multi-tenant application patterns

## Tenant isolation

Resolve tenant identity from the authenticated session, not a user-controlled request parameter. Authorize access before querying or mutating data. In a shared database, use tenant-scoped keys and enforce row-level security where appropriate; schema-per-tenant designs require safe identifier handling and controlled migrations.

## Reliability

Use transaction boundaries for related writes. An outbox can persist business events alongside state changes, allowing workers to publish them asynchronously. Consumers should be idempotent, because duplicate delivery is possible.

## Observability and operations

Track latency, error rate, queue depth and resource saturation. Use correlation IDs without embedding credentials or customer content in logs. Validate backups through restore exercises and rehearse migration rollback procedures.

## Verification checklist

- Cross-tenant reads and writes are rejected.
- Duplicate events do not create duplicate side effects.
- Migration failures can be recovered without losing tenant data.
- Logs and metrics contain no secrets.
- Backup restoration is tested in isolation.

These are generic design recommendations, not a description of any private product architecture.
