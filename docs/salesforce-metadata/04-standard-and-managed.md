---
title: Standard & Managed-Package Objects
captured: 2026-06-19
tags: [salesforce, audit, standard, managed-package, storage]
---

# 04 — Standard Objects (custom fields) + Managed Packages

> Live connector 2026-06-19. Hub: [[README]] · [[01-object-inventory]] · [[00-org-snapshot]]

## Core standard objects — customization footprint
Total vs **org custom (`__c`)** field counts. Standard SF fields omitted (documented by Salesforce).
Account is by far the most customized object in the org.

| Object | Records | Total fields | Custom fields |
|---|---|---|---|
| **Account** | 69,320 | 510 | **449** |
| **Case** | (high) | 412 | **361** |
| **User** | 570 | 480 | **287** |
| Contact | (high) | 251 | 178 |
| Lead | (high) | 172 | 114 |
| Opportunity | (high) | 141 | 96 |
| Event | (high) | 116 | 64 |
| Task | (high) | 108 | 64 |
| Contract | — | 61 | 12 |
| Campaign | — | 42 | 5 |
| ContentVersion | — | 46 | 2 |
| EmailMessage | — | 45 | 2 |
| Pricebook2 / Product2 / Entitlement / ContentDocument / CampaignMember | — | 14–36 | 0 |

> Full per-field lists for Account (449), Case (361), User (287), Contact, Lead, Opportunity, Event, Task
> are generated in the connector run and can be exported on request (large — see note at bottom).

## Managed-package objects in use (111 total)
The org runs many managed packages. High-volume objects below are the most likely
**data-storage consumers** (relevant to the 99.7% storage warning in [[00-org-snapshot]]):

| Object | Records | Package |
|---|---|---|
| `voice_connector__VCLog__c` | **1,048,141** | Voice Connector |
| `voice_connector__VCCallRecording__c` | **573,642** | Voice Connector |
| `miedge_crm__PC_Detail__c` | 196,537 | miEdge |
| `dupcheck__dcIndex__c` | 194,954 | Plauti DupCheck |
| `voice_connector__VCCall__c` | 193,100 | Voice Connector |
| `dupcheck__dc3Duplicate__c` | 69,122 | Plauti DupCheck |
| `miedge_crm__EB_Detail__c` | 69,023 | miEdge |
| `miedge_crm__Master_MSID__c` | 60,485 | miEdge |
| `dupcheck__dcTemp__c` | 57,929 | Plauti DupCheck |
| `qsyd_FE__FileExplorerFile__c` | 51,482 | File Explorer |
| `dupcheck__dcDiscard__c` | 47,154 | Plauti DupCheck |
| `aircall__Aircall_AI__c` | 29,195 | Aircall |
| `DOZISF__ZoomInfo__c` | 9,912 | ZoomInfo |
| `fpro__FieldPro__c` | 7,042 | FieldPro |
| `dupcheck__dcAudit__c` | 5,016 | Plauti DupCheck |

> **Storage action:** Voice Connector logs (~1.6M rows across VCLog/VCCallRecording/VCCall),
> Plauti DupCheck working tables (~370k rows of dcIndex/dcTemp/dcDiscard/dc3Duplicate — these are
> transient dedup artifacts, often safe to purge), and miEdge detail (~326k rows) dominate. Purging
> or archiving DupCheck temp/discard tables and old Voice Connector logs is the fastest path to
> relieving the 99.7% data-storage pressure.

Other packages present (lower volume): FSL (Field Service), Calendly, ActiveCampaign, Loop/Nintex
DocGen, Field Trip, iahelp (In-App Help), Rollup Helper (`rh2__`), Plauti Verify (`recordval__`),
Sonar, pw_cc (CountryComplete), permissioner, sf_devops, CodeBuilder. Full inventory: [[01-object-inventory]].

---
### Completeness note
Business custom objects (25) have **full** field detail in [[03-business-custom-fields]].
Standard objects and managed-package objects are summarized here (field counts + records).
The complete field-by-field export for all 153 in-use objects (6,369 fields) was generated in the
connector session; the full standard/managed field lists can be regenerated and exported on request.
