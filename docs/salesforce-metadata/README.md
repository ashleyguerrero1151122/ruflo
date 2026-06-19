# Salesforce Data Model — Whiteboard Risk (Workers' Comp)

**Org:** whiteboardrisk.my.salesforce.com (`00D3t000003yapwEAA`)
**Mapped:** 2026-06-19 via live Salesforce connector (Composio)
**Scope:** Workers'-comp objects (policy / loss run / claims). 333 total custom objects in org.

> This folder contains METADATA ONLY (object + field definitions). No claimant
> records or PII are stored here.

---

## Object relationship map

```
Account  (employer / policyholder)
  └── WB_Policy__c          "Policy"            (keyPrefix a0J)
        └── Loss_Run__c     "Loss Run" (request tracker, monthly)   (a28)
              └── Loss_Run_Results__c  "Loss Run Results" = CLAIMS  (a51)
```

- **Claims live in `Loss_Run_Results__c`** — there is NO `Claim__c` object.
- `Loss_Run__c` is a monthly loss-run *request* tracker, not the claim data itself.
- ~49,335 claim rows total (Closed 40,456 / Open 6,676 / Needs Review 1,508 / Reopened 413 / blank 282).

---

## WB_Policy__c — "Policy" (37 fields)
| API name | Label | Type | Notes |
|---|---|---|---|
| Name | Policy Name | string | |
| Policy_Number__c | Policy Number | string | |
| Status__c | Status | picklist | |
| Effective_Date__c | Effective Date | date | |
| Expiration_Date__c | Expiration Date | date | |
| WC_Renewal_Date__c | WC Renewal Date | date | |
| Date_First_Written__c | Date First Written | date | |
| Premium__c | Premium | currency | |
| CA_Policy_Premium__c | CA Policy Premium | currency | |
| Payroll__c | Payroll | currency | |
| Account__c | Account | reference → Account | rel: Account__r |
| Issuing_Carrier__c | Issuing Carrier | reference → Account | rel: Issuing_Carrier__r |
| Billing_Company__c | Billing Company | reference → Account | rel: Billing_Company__r |
| Line_of_Coverage__c | Line of Coverage | multipicklist | |
| Covered_States__c | Covered States | multipicklist | |
| Out_of_State_Policy__c | Out of State Policy | boolean | |
| Current_Policy_Term__c | Current Policy Term | boolean | |
| Days_to_Renewal__c | Days to Renewal | double | |
| Loss_Run_Retrieval_Method__c | Loss Run Retrieval Method | picklist | |
| Loss_Run_Request_Email__c | Loss Run Request Email | string | |
| A_M_Representation__c | A&M Representation? | boolean | |

## Loss_Run__c — "Loss Run" / request tracker (22 fields)
| API name | Label | Type | Notes |
|---|---|---|---|
| Name | Loss Run Name | string | |
| Policy__c | Policy | reference → WB_Policy__c | rel: Policy__r |
| Account__c | Account | reference → Account | rel: Account__r |
| Status__c | Status | picklist | |
| Date_Requested__c | Month Requested | date | |
| Date_to_Request__c | Date to Request | date | |
| Day_to_Request__c | Day to Request | double | |
| Carrier__c | Issuing Carrier | string | |
| Billing_Carrier__c | Billing Carrier | string | |
| Loss_Run_Notes__c | Loss Run Notes | textarea | |

## Loss_Run_Results__c — "Loss Run Results" = CLAIMS (37 fields)
| API name | Label | Type | Notes |
|---|---|---|---|
| Name | Loss Run Results Name | string | |
| Claim_Number__c | Claim Number | string | |
| Claimant_Name__c | Claimant Name | string | |
| Status__c | Status | picklist | Closed / Open Claim / Needs Review / Reopened |
| Date_of_Loss__c | Date of Loss | date | |
| Date_Closed__c | Date Closed | date | |
| Date_Reported_to_Carrier_LR__c | Date Reported to Carrier | date | |
| Account_Name__c | Account Name | string | text |
| Policy_Number__c | Policy Number | reference → WB_Policy__c | rel: Policy_Number__r |
| Policy_Number_Text__c | Policy Number | string | text copy |
| Case__c | Case | reference → Case | rel: Case__r |
| Triggering_Loss_Run__c | Triggering Loss Run | reference → Loss_Run__c | rel: Triggering_Loss_Run__r |
| **Paid_Medical__c** | Paid Medical | currency | money |
| **Medical_Reserves__c** | Medical Reserves | currency | money |
| **Paid_Indemnity__c** | Paid Indemnity | currency | money |
| **Indemnity_Reserve__c** | Indemnity Reserve | currency | money |
| **ALE_Cost__c** | ALE Cost | currency | money |
| Indemnity_Incurred_LR__c | Indemnity Incurred | currency | indemnity only |
| Cause_Nature_of_Injury_New_Formula_LR__c | Cause/Nature of Injury | string (formula) | |
| Injury_Description_and_Details__c | Injury Description | textarea | |
| Claimant_Age_LR__c | Claimant Age | double | |
| Claimant_Date_of_Birth_LR__c | Claimant DOB | date | |
| Claimant_Date_of_Hire_LR__c | Claimant Date of Hire | date | |
| Claimant_Job_Title_LR__c | Claimant Job Title | string | |

### ⚠️ Total Incurred formula (no single field exists)
```
Total Incurred = Paid_Medical__c + Medical_Reserves__c
               + Paid_Indemnity__c + Indemnity_Reserve__c + ALE_Cost__c
```

---

## Other comp/insurance objects in org
| API name | Label |
|---|---|
| Avg_Claim_Cost__c | Avg Claim Cost |
| Carrier_Rating__c | Carrier Rating |
| License__c | Insurance Licenses |
| Internal_Policy_Tracker__c | Internal Policy |
| Loss_Run_Extraction_Prompt__mdt | Loss Run Extraction Prompt (metadata) |

---

## Validated SOQL (tested live 2026-06-19)

**Claims by status**
```sql
SELECT COUNT(Id) Cnt, Status__c FROM Loss_Run_Results__c GROUP BY Status__c
```

**Policies expiring in 60 days**
```sql
SELECT Name, Policy_Number__c, Account__r.Name, Premium__c, Expiration_Date__c, WC_Renewal_Date__c
FROM WB_Policy__c
WHERE Expiration_Date__c = NEXT_N_DAYS:60
ORDER BY Expiration_Date__c
```

**Open claims with incurred total**
```sql
SELECT Claim_Number__c, Claimant_Name__c, Account_Name__c, Status__c, Date_of_Loss__c,
       Paid_Medical__c, Medical_Reserves__c, Paid_Indemnity__c, Indemnity_Reserve__c, ALE_Cost__c
FROM Loss_Run_Results__c
WHERE Status__c = 'Open Claim'
ORDER BY Date_of_Loss__c
```

**Loss run for one employer (last 3 years), high-severity first**
```sql
SELECT Claim_Number__c, Date_of_Loss__c, Status__c,
       Paid_Medical__c, Medical_Reserves__c, Paid_Indemnity__c, Indemnity_Reserve__c, ALE_Cost__c
FROM Loss_Run_Results__c
WHERE Account_Name__c = 'ACME Roofing' AND Date_of_Loss__c = LAST_N_YEARS:3
ORDER BY Date_of_Loss__c
```

**High-severity open claims (compute total in app, > $50k)** — sum the 5 money fields after retrieval, since SOQL can't filter on an expression of multiple fields without a formula field.
