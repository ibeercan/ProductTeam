# NFR checklist

For each category: either write a measurable requirement into `spec.md` section 6, or raise an open question. Do not leave a category silently empty.

| Category | Ask | Example measurable target |
|----------|-----|---------------------------|
| Performance | Response times, throughput, data volumes | p95 < 300 ms at 50 rps; report builds in < 30 s for 1M rows |
| Availability | Uptime expectations, maintenance windows | 99.5% monthly; planned downtime < 2 h/month |
| Reliability | Failure behaviour, recovery, data loss tolerance | RPO 15 min, RTO 2 h; no data loss on restart |
| Security | AuthN/AuthZ, data classification, secrets, audit trail | RBAC roles listed; PII encrypted at rest; actions logged |
| Privacy / Compliance | Applicable data-protection rules, retention | Personal data retained 1 year, then deleted; consent captured |
| Scalability | Growth expectations, horizontal scaling | Handles 10x current load by adding instances |
| Observability | Logs, metrics, alerts needed to operate | Error rate > 1% pages the on-call within 5 min |
| Maintainability | Environments, IaC, documentation expectations | Deploys via CI from main; runbook exists |
| Usability / Accessibility | Accessibility level, supported devices/browsers | WCAG 2.1 AA for user-facing web UI |

Guidance: pick the 3–5 categories that matter for this initiative and set real targets; the rest get a one-line "not applicable because…" or an open question. A blank section is a defect.
