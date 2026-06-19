---
title: Business Custom Objects — Fields
captured: 2026-06-19
tags: [salesforce, audit, fields, business-custom]
---

# 03 — Business Custom Objects: Full Fields

> Live connector 2026-06-19. Hub: [[README]] · [[01-object-inventory]] · [[02-data-model-claims]]
> All 25 in-use, org-built custom objects (no managed-package namespace). Deprecated/unused excluded.
> Format: `API Name` — Label *(type → reference)*.

## Activity_Tracker__c
*Activity Tracker* · records 33 · 25 fields · prefix a1u
Key custom fields: `Is_Active__c` (boolean), `Tasks__c`, `Total_Calls__c`, `Total_Meetings__c`, `Total_Meetings_Rescheduled__c`, `Total_New_In_person_Meetings__c`, `Total_New_Meeting_Cancellations__c`, `Total_New_Meeting_No_Shows__c`, `Total_New_Meetings_That_Haven_t_Happened__c`, `Total_New_Meetings__c`, `Total_New_Meetings_that_Met__c`, `Total_New_Phone_Meetings__c` (all double), `User_Id__c` (string), `User__c` (→User).

## After_Care_Instructions__c
*After Care Instructions* · records 12 · 13 fields · prefix a4a
Custom: `ACI_Details__c` (textarea), `ACI_Language__c` (picklist).

## Avg_Claim_Cost__c
*Avg Claim Cost* · records 89 · 13 fields · prefix a1t — `Name` = Cause/Nature of Injury
Custom: `CA_Avg_Claim_Cost__c` (currency).

## CA_Cities_Counties__c
*CA Cities & Counties* · records 1,241 · 14 fields · prefix a1z
Custom: `County__c` (string), `City__c` (string), `In_Person_Meeting_Territory__c` (boolean).

## CCO_Contact__c
*CCO Contact* · records 852 · 12 fields · prefix a4d
Custom: `CCORelatedContact__c` (→Contact), `CCO_Interaction__c` (→CCO_Interaction__c), `CCO_Account_ID__c` (string).

## CCO_Interaction__c
*CCO Interaction* · records 619 · 22 fields · prefix a4b
Custom: `Account_CCO__c` (→Account), `Establishment_Name_CCO__c` (string), `Interaction_Date_CCO__c` (date), `Was_Broker_Present_CCO__c` (boolean), `Interaction_Cost_CCO__c` (currency), `Interaction_Notes_CCO__c` (textarea), `Interaction_Type_Other_CCO__c` (string), `CCO_Level__c` (picklist), `Interaction_Type_CCO__c` (multipicklist), `Type_Contains_Other__c` (boolean).

## Carrier_Rating__c
*Carrier Rating* · records 2 · 23 fields · prefix a29
Custom: `Carrier__c` (→Account), `Claim_Manager__c` (→User), `Comments__c` (textarea), `Adjuster_Accessibility__c`, `Broker_Liaison_Effectiveness__c`, `Claimant_Communication__c`, `Communication__c`, `Ease_of_Collaboration__c`, `Receptiveness_to_Suggestions__c`, `USD_Reporting_Department__c` (all picklist), `Total_Score__c` (double).

## Cognisure_Files__c
*Cognisure Files* · records 2,517 · 24 fields · prefix a2k — (AI doc-extraction integration)
Custom: `Carrier__c`, `Confidence_Score__c`, `DocumentCategory__c`, `EntityName__c` (string), `Insured_Name__c` (textarea), `Reason__c` (string), `Synced__c` (boolean), `UploadedOn__c` (datetime), `bundleId__c`, `documentType__c`, `fileGUID__c`, `fileOriginalName__c`, `fileReceivedChannel__c` (string).

## Employee__c
*Employee* · records 51 · 50 fields · prefix a5r (has RecordTypes)
Custom highlights: `Start_Date__c`, `Offboard_Date__c` (date), `Supervisor_Name__c`, `Department__c`, `Role__c`, `Title__c`, `First_Name__c`, `Last_Name__c` (string), `Salesforce_User__c`, `Manager__c`, `Current_User_is_Owner__c` (boolean), `User__c`, `Manager_Lookup__c` (→Employee__c), `Email__c` (email), `Phone__c`, `Work_Phone__c` (phone), `Employee_Profile_Picture__c` (url), `Enneagram_Primary_Summary__c`, `Enneagram_Secondary_Summary__c`, `Commission_Notes__c` (textarea), `Commission_Tier__c` (picklist), `New_Commission_Rate__c`, `Renewal_Commission_Rate__c` (percent), `Enneagram_Primary_Number__c`, `Enneagram_Secondary_Number__c` (multipicklist), `Length_of_Service__c`, `Apparel_Top_Size__c` (string), `Qty_of_Devices__c` (double), `Shipping_Address__c` (address + components).

## Equipment__c
*Equipment* · records 1 · 19 fields · prefix a6L
Custom: `Device_OS__c`, `Device_Name__c` (string), `Device_Type__c` (picklist), `Manufacturer__c`, `Model__c`, `Serial__c` (string), `Employee__c` (→Employee__c).

## ISR_First_Last_Call_Per_Day__c
*ISR First/Last Call Per Day* · records 1,242 · 14 fields · prefix a5q
Custom: `Date__c` (date), `First_Call_Time__c`, `Last_Call_Time__c` (time), `Calls_Made__c`, `Avg_Call_Duration__c` (double).

## Incident_Service_Usage__c
*Incident Service Usage* · records 5,725 · 20 fields · prefix a2Q
Custom: `Case__c` (→Case), `Incident_Service__c` (picklist), `Number_of_Calls_in_Triage_Phone_Service__c`, `Number_of_Technician_Dispatches__c` (double), `Is_Generated__c` (boolean), `Service_Type_Ortholive__c`, `WITs_Technician_Name__c` (picklist), `OrthoLive_Cost__c`, `Client_Cost__c`, `Incident_Service_Revenue__c` (currency), `AccountId__c` (string), `After_Hours__c` (boolean).

## Industry_Codes__c
*Industry Code* · records 2,569 · 16 fields · prefix a6N
Custom: `Type__c` (picklist), `Description__c`, `Industry_Title__c`, `Code__c` (string).

## Internal_Policy_Tracker__c
*Internal Policy* · records 13 · 21 fields · prefix a50 — (WB's own insurance policies)
Custom: `Policy_Number__c` (string), `Insurance_Lines__c` (multipicklist), `Effective_Date__c`, `Expiration_Date__c` (date), `Issuing_Carrier__c` (→Account), `Issuing_Agent__c` (string), `Premium__c` (currency), `Status__c`, `Type__c` (picklist).

## Letter_Tracking__c
*Letter Tracking* · records 110 · 21 fields · prefix a5P
Custom: `Date_Sent__c` (date), `Status__c` (picklist), `Mailing_Address__c` (address + components), `Undeliverable_Reason__c` (textarea), `Contact__c` (→Contact).

## License__c
*Insurance Licenses* · records 59 · 24 fields · prefix a3W (has RecordTypes)
Custom: `Expiration_Date__c` (date), `License_Number__c`, `Licensing_State__c` (string), `Insurance_Lines__c` (multipicklist), `Type_del__c` (picklist), `License_Owner__c` (→User), `License_Owner_Non_SF__c` (string), `Owner_Salesforce_Access__c`, `Owner_Residency__c`, `Status__c` (picklist), `Expiration_Date_Approaching__c` (boolean).

## Loss_Run_Results__c  ⭐ CLAIMS
*Loss Run Results* · records 49,335 · 37 fields · prefix a51 — see [[02-data-model-claims]]
Money: `Paid_Medical__c`, `Medical_Reserves__c`, `Paid_Indemnity__c`, `Indemnity_Reserve__c`, `ALE_Cost__c`, `Indemnity_Incurred_LR__c` (currency).
Key: `Claim_Number__c`, `Claimant_Name__c`, `Account_Name__c`, `Policy_Number_Text__c` (string), `Policy_Number__c` (→WB_Policy__c), `Case__c` (→Case), `Triggering_Loss_Run__c` (→Loss_Run__c), `Date_of_Loss__c`, `Date_Closed__c`, `Loss_Value_Date__c`, `Claimant_Date_of_Birth_LR__c`, `Claimant_Date_of_Hire_LR__c`, `Date_Reported_to_Carrier_LR__c` (date), `Status__c` (picklist), `Claimant_Age_LR__c` (double), `Injury_Description_and_Details__c`, `Loss_Run_Review__c` (textarea), `Fields_to_Review__c`, `Cause_Nature_of_Injury_New_Formula_LR__c`, `Claimant_Job_Title_LR__c` (string).

## Loss_Run__c
*Loss Run* (monthly request tracker) · records 7,073 · 22 fields · prefix a28
Custom: `Policy__c` (→WB_Policy__c), `Account__c` (→Account), `Status__c` (picklist), `Date_Requested__c` (date, "Month Requested"), `Loss_Run_Notes__c`, `VA_Loss_Run_Cheatsheet__c` (textarea), `Carrier__c`, `Billing_Carrier__c` (string), `Day_to_Request__c` (double), `Date_to_Request__c` (date).

## Non_Profit_Placement__c
*Non-Profit Placement* · records 38 · 18 fields · prefix a3U
Custom: `Non_Profit_Vendor__c` (picklist), `Placement_Description__c` (textarea), `Placement_Stage__c` (picklist), `Start_Date__c`, `End_Date__c` (date), `Payment_Responsibility__c` (picklist), `Vendor_Cost__c`, `WB_Non_Profit_Revenue__c` (currency), `Related_Case__c` (→Case).

## Safety_Walkthrough__c
*Marin Safety Walkthrough Checklist* · records 56 · 22 fields · prefix a2A
Custom: `Area__c` (picklist), `Interaction_With__c` (string), `At_Risk_Behavior__c`, `PPE__c`, `Housekeeping__c`, `Lifting_Mechanics__c`, `Training_Recap__c` (picklist), `Notes__c` (textarea), `Total_Score__c` (double), `Date_Completed__c` (date).

## Subsidiary__c
*Subsidiary* · records 35 · 21 fields · prefix a2E
Custom: `Location_Address__c` (string), `Account__c` (→Account), `Location_Address_Custom__c` (address + components), `Location_Address_Formula__c` (string formula).

## USLH_Case__c  ⭐ (USL&H claims — full claim object, 136 fields)
*USL&H Case* · records 149 · 136 fields · prefix a2P (has RecordTypes)
This is the most field-rich business object — a full workers'-comp/USL&H claim record. Money: `ALE_Cost__c`, `Indemnity_Reserves__c`, `Medical_Reserves__c`, `Paid_Indemnity__c`, `Paid_Medical__c`, `Indemnity_Incurred__c`, `Medical_Incurred__c`, `Total_Incurred__c`, `Total_Paid__c`, `Total_Reserves__c`, `ODG_Best_Practice_Indemnity__c`, `ODG_Best_Practice_Medical__c`, `ODG_Max_Indemnity__c`, `ODG_Max_Medical__c`, `ODG_Typical_Indemnity__c`, `ODG_Typical_Medical__c` (currency). Relationships: `Policy__c` (→WB_Policy__c), `Account__c` (→Account), `Adjuster__c` (→Contact), `Cause_Nature_of_Injury_New__c` (→Avg_Claim_Cost__c). Plus ~100 claim-detail fields (claimant demographics, injury description, body parts, treatment, work status, attorneys, dates, ODG durations, etc.). **Note: USLH_Case__c HAS a native `Total_Incurred__c` currency field** (unlike Loss_Run_Results__c which must be summed).

## WB_Policy__c  ⭐ POLICY
*Policy* · records 8,647 · 37 fields · prefix a0J — see [[02-data-model-claims]]
Custom: `Status__c`, `Loss_Run_Retrieval_Method__c` (picklist), `Policy_Number__c`, `Old_Policy_ID__c`, `MPN_Lookup__c`, `Loss_Run_Request_Email__c` (string), `Effective_Date__c`, `Expiration_Date__c`, `Date_First_Written__c`, `WC_Renewal_Date__c` (date), `Premium__c`, `CA_Policy_Premium__c`, `Payroll__c` (currency), `Issuing_Carrier__c`, `Billing_Company__c`, `Account__c` (→Account), `Line_of_Coverage__c`, `Covered_States__c` (multipicklist), `A_M_Representation__c`, `Out_of_State_Policy__c`, `TF_CaliforniaIsSelected__c`, `Current_Policy_Term__c` (boolean), `Days_to_Renewal__c` (double), `Preferred_Clinic_Address__c`, `Preferred_Clinic_and_Address__c` (textarea).

## Work_Status_Report__c
*Work Status Report Tracking* · records 3,517 · 21 fields · prefix a2V
Custom: `Case__c` (→Case), `Last_Office_Visit__c`, `Next_Office_Visit__c` (date), `Current_Work_Status__c`, `Return_to_Work_Method__c` (picklist), `Work_Restrictions__c`, `Diagnosis__c`, `Clinic_or_Specialist_Information_c__c`, `Treatment_Plan__c` (textarea), `Treating_Physician__c` (string), `Days_on_Full_Duty__c`, `Days_on_Job_Transfer_or_Restriction__c`, `Days_Way_from_Work__c` (double).

## X_Mod_History__c
*X-Mod History* · records 11 · 18 fields · prefix a2W
Custom: `Account__c` (→Account), `RED_Year__c`, `X_Mod_Eff__c`, `X_Mod__c`, `Number_of_Rerates__c` (double), `X_Mod_Status__c` (picklist), `Rerate_Reason__c` (textarea), `Status_Date__c` (date).
