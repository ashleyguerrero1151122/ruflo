---
title: Org Snapshot
captured: 2026-06-19
tags: [salesforce, audit, org-snapshot]
---

# 00 — Org Snapshot

> Source: live Salesforce connector, 2026-06-19. Metadata + org insights only.
> Hub: [[README]] · Related: [[01-object-inventory]] · [[02-data-model-claims]]

## Org
| | |
|---|---|
| Name | Whiteboard Risk & Insurance Services |
| Org ID | `00D3t000003yapwEAA` |
| Edition | Enterprise Edition |
| Type | **Production** (not sandbox) |
| Instance | USA566 |
| Created | 2020-08-13 |
| Locale / Language | en_US / en_US |
| Fiscal year starts | January |
| API version observed | v62.0 |

## 🚨 Storage & key limits
| Limit | Used | Max | % |
|---|---|---|---|
| **Data Storage (MB)** | **14,428** | **14,470** | **99.7%** ⚠️ |
| File Storage (MB) | 79,554 | 115,492 | 68.9% |
| Daily API Requests | 53,914 | 184,000 | 29.3% |
| Daily Bulk API Batches | 790 | 15,000 | 5.3% |
| Permission Sets (platform limit) | 201 | 1,500 | 13.4% |

**Action:** Data storage is effectively full (~42 MB free). Largest data object is
`Loss_Run_Results__c` (~49,335 rows). Options: archive/delete aged loss-run & claim
rows, purge old records on high-volume standard objects, buy more storage, or move
cold data to Big Objects. This is the #1 priority.

## Users & licenses
- **Users:** 236 active · 334 inactive (570 total)
- **Salesforce (full CRM) license: 49 / 49 used — MAXED.** Cannot add full users without buying more or deactivating.

**Notable user licenses (used / total):**
| License | Used | Total |
|---|---|---|
| Salesforce | 49 | 49 |
| Customer Community Plus Login | 148 | 3,000 |
| Einstein Agent | 13 | 802 |
| Guest User License | 14 | 25 |
| Salesforce Integration | 1 | 5 |
| Customer Community Plus | 0 | 25 |

## Active users per profile
| Count | Profile |
|---|---|
| 148 | New Customer Community Plus Login User |
| 14 | Claims |
| 13 | Einstein Agent User |
| 11 | Producer |
| 9 | Triage |
| 7 | Inside Sales |
| 5 | (none) |
| 4 | System Administrator |
| 3 | Marketing Manager for Onboarding |
| 1 ea | ~20 service/integration/portal profiles |

> 4 active System Administrators — verify each is still needed (security/least-privilege).

## Automation & customization footprint
| Asset | Count |
|---|---|
| Custom fields | 41,820 |
| Apex classes | 8,436 |
| Apex triggers | 250 |
| Flows (total / active) | 641 / 463 |
| Validation rules | 180 |
| Permission sets (non-profile) | 513 |

## Permission-set licenses (heavily provisioned)
The org has 130+ permission-set licenses in use — dominated by **Agentforce / Einstein /
Data Cloud / Field Service / CRM Analytics**. Highlights: Agentforce (Default) 48/100,
Data Cloud 31/200000, Standard Einstein Activity Capture 51/100, Einstein Prompt Templates
58/100122, CRM Analytics for Community Members 147/150 (near cap), Einstein Conversation
Insights 30/30 (capped). Full list captured in the connector run.

## Insights / recommendations
1. **Storage (urgent):** at 99.7%. Archive aged claims/loss-run data or expand storage.
2. **Licenses:** full Salesforce seats maxed (49/49); 334 inactive users already freeing seats.
3. **Sprawl / tech debt:** 513 permission sets + 8,436 Apex classes + 641 flows + 247
   managed-package objects (Agentforce, Einstein, Data Cloud, FSL, Avonni, Sweep, ZoomInfo,
   Nintex, DataGroomr, Plauti…). Worth a managed-package + permission-set cleanup audit.
4. **CRM Analytics for Community Members** at 147/150 — near cap, monitor.
5. **Security:** review the 4 System Administrators and the many 1-off integration profiles.
