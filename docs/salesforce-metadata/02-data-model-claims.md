---
title: Data Model — Policy / Loss Run / Claims
captured: 2026-06-19
tags: [salesforce, audit, data-model, claims]
---

# 02 — Data Model: Policy / Loss Run / Claims

> Source: live connector, 2026-06-19. Hub: [[README]] · Related: [[00-org-snapshot]] · [[01-object-inventory]]

## Relationship map
```
Account (employer / policyholder)
  └── WB_Policy__c          "Policy"             (keyPrefix a0J)
        └── Loss_Run__c     "Loss Run" (monthly request tracker)   (a28)
              └── Loss_Run_Results__c   "Loss Run Results" = CLAIMS (a51)
```
- **Claims live in `Loss_Run_Results__c`** — there is NO `Claim__c` object.
- `Loss_Run__c` tracks the monthly loss-run *request*, not the claim data.
- ~49,335 claim rows: Closed 40,456 · Open Claim 6,676 · Needs Review 1,508 · Reopened 413 · blank 282.

## WB_Policy__c — "Policy"
Key fields: `Name`, `Policy_Number__c`, `Status__c`, `Effective_Date__c`, `Expiration_Date__c`,
`WC_Renewal_Date__c`, `Date_First_Written__c`, `Premium__c`, `CA_Policy_Premium__c`, `Payroll__c`,
`Account__c`→Account, `Issuing_Carrier__c`→Account, `Billing_Company__c`→Account,
`Line_of_Coverage__c` (multipicklist), `Covered_States__c` (multipicklist), `Out_of_State_Policy__c`,
`Current_Policy_Term__c`, `Days_to_Renewal__c`, `Loss_Run_Retrieval_Method__c`, `Loss_Run_Request_Email__c`.

## Loss_Run__c — request tracker
Key fields: `Name`, `Policy__c`→WB_Policy__c, `Account__c`→Account, `Status__c`,
`Date_Requested__c`, `Date_to_Request__c`, `Day_to_Request__c`, `Carrier__c`, `Billing_Carrier__c`,
`Loss_Run_Notes__c`.

## Loss_Run_Results__c — CLAIMS
Key fields: `Name`, `Claim_Number__c`, `Claimant_Name__c`, `Status__c`, `Date_of_Loss__c`,
`Date_Closed__c`, `Date_Reported_to_Carrier_LR__c`, `Account_Name__c`,
`Policy_Number__c`→WB_Policy__c, `Case__c`→Case, `Triggering_Loss_Run__c`→Loss_Run__c,
`Injury_Description_and_Details__c`, `Claimant_Age_LR__c`, `Claimant_Date_of_Birth_LR__c`,
`Claimant_Job_Title_LR__c`.

**Money fields:** `Paid_Medical__c`, `Medical_Reserves__c`, `Paid_Indemnity__c`,
`Indemnity_Reserve__c`, `ALE_Cost__c`, `Indemnity_Incurred_LR__c` (indemnity only).

### ⚠️ Total Incurred (no single field)
```
Total Incurred = Paid_Medical__c + Medical_Reserves__c
               + Paid_Indemnity__c + Indemnity_Reserve__c + ALE_Cost__c
```

## Validated SOQL (tested live 2026-06-19)
```sql
-- Claims by status
SELECT COUNT(Id) Cnt, Status__c FROM Loss_Run_Results__c GROUP BY Status__c

-- Policies expiring in 60 days
SELECT Name, Policy_Number__c, Account__r.Name, Premium__c, Expiration_Date__c, WC_Renewal_Date__c
FROM WB_Policy__c WHERE Expiration_Date__c = NEXT_N_DAYS:60 ORDER BY Expiration_Date__c

-- Loss run for one employer, last 3 years
SELECT Claim_Number__c, Date_of_Loss__c, Status__c,
       Paid_Medical__c, Medical_Reserves__c, Paid_Indemnity__c, Indemnity_Reserve__c, ALE_Cost__c
FROM Loss_Run_Results__c
WHERE Account_Name__c = 'ACME Roofing' AND Date_of_Loss__c = LAST_N_YEARS:3
ORDER BY Date_of_Loss__c
```
