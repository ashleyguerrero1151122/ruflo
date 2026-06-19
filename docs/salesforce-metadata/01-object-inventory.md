---
title: Object Inventory
captured: 2026-06-19
tags: [salesforce, audit, objects]
---

# 01 — Object Inventory

> Source: live connector, 2026-06-19. Hub: [[README]] · Related: [[00-org-snapshot]] · [[02-data-model-claims]]

## Totals
| Category | Count |
|---|---|
| **All objects** | **3,181** |
| Standard / system | 2,848 |
| Custom (`__c`/namespaced) | 333 |
| └ Managed-package custom | 247 |
| └ Platform/own (events, metadata types, business) | 86 |
| Business custom objects (own `__c`) | ~27 |

Managed-package namespaces present include: `FSL__` (Field Service), `Sweep__`,
`ortoo_act__`, `sf_devops__`, `avxp__`/`avdynamic__` (Avonni), `miedge_crm__`,
`voice_connector__`, `qsydApps_AO__`, `DOZISF__`, `csv2sf__`, `rh2__` (Rollup Helper),
`personalizeAny__`, `Loop__` (Nintex), `CMTD__`.

## Business custom objects (own, non-managed)
| API name | Label | Queryable |
|---|---|---|
| WB_Policy__c | Policy | ✅ |
| Loss_Run__c | Loss Run (request tracker) | ✅ |
| Loss_Run_Results__c | Loss Run Results (= CLAIMS) | ✅ |
| Avg_Claim_Cost__c | Avg Claim Cost | ✅ |
| Carrier_Rating__c | Carrier Rating | ✅ |
| License__c | Insurance Licenses | ✅ |
| Internal_Policy_Tracker__c | Internal Policy | ✅ |
| USLH_Case__c | USL&H Case | ✅ |
| X_Mod_History__c | X-Mod History | ✅ |
| Subsidiary__c | Subsidiary | ✅ |
| Employee__c | Employee | ✅ |
| Equipment__c | Equipment | ✅ |
| Industry_Codes__c | Industry Code | ✅ |
| Incident_Service_Usage__c | Incident Service Usage | ✅ |
| Letter_Tracking__c | Letter Tracking | ✅ |
| Non_Profit_Placement__c | Non-Profit Placement | ✅ |
| Safety_Walkthrough__c | Marin Safety Walkthrough Checklist | ✅ |
| Work_Status_Report__c | Work Status Report Tracking | ✅ |
| Activity_Tracker__c | Activity Tracker | ✅ |
| After_Care_Instructions__c | After Care Instructions | ✅ |
| CCO_Contact__c | CCO Contact | ✅ |
| CCO_Interaction__c | CCO Interaction | ✅ |
| CA_Cities_Counties__c | CA Cities & Counties | ✅ |
| ISR_First_Last_Call_Per_Day__c | ISR First/Last Call Per Day | ✅ |
| Cognisure_Files__c | Cognisure Files | ✅ |
| ZoomInfoCompany__x / ZoomInfoContact__x | ZoomInfo (external objects) | ✅ |

> Loss-run / claims objects are detailed in [[02-data-model-claims]].
> Full field-level notes per object: see `objects/` (generated on request — see hub).
