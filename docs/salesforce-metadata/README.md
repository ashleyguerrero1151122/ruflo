---
title: Salesforce Org Audit — Whiteboard Risk
org: Whiteboard Risk & Insurance Services
org_id: 00D3t000003yapwEAA
edition: Enterprise
captured: 2026-06-19
tags: [salesforce, audit, MOC]
---

# 🗂️ Salesforce Org Audit — Map of Content

Live audit of **Whiteboard Risk & Insurance Services** (`whiteboardrisk.my.salesforce.com`),
pulled via the Salesforce connector. **Metadata + org insights only — no business records / PII.**

## Notes in this audit
- [[00-org-snapshot]] — limits, **storage**, licenses, users, permissions, automation footprint
- [[01-object-inventory]] — all 3,181 objects categorized; the business custom objects
- [[02-data-model-claims]] — policy / loss-run / claims data model + validated SOQL
- [[03-business-custom-fields]] — full fields for all 25 business custom objects
- [[04-standard-and-managed]] — standard-object custom fields + managed packages + **storage culprits**
- `whiteboardrisk-data-model.json` — structured field metadata (claims model)

## 🚨 Top findings (see [[00-org-snapshot]])
1. **Data storage 99.7% full** (14,428 / 14,470 MB — ~42 MB free). Most urgent.
2. **Salesforce (full CRM) licenses maxed: 49 / 49.**
3. **Tech-debt / sprawl:** 8,436 Apex classes · 41,820 custom fields · 641 flows · 513 permission sets · 247 managed-package objects.

> Captured 2026-06-19. Re-run the connector to refresh; this is a point-in-time snapshot.
