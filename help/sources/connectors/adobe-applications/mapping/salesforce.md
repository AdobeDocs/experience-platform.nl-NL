---
keywords: Experience Platform;home;populaire onderwerpen;Salesforce;salesforce;field mapping;Field mapping;marketo;B2B;b2b
title: Salesforce-toewijzingsvelden
description: De onderstaande tabellen bevatten de toewijzingen tussen Salesforce-bronvelden en de bijbehorende XDM-velden.
source-git-commit: d0efc8ffab33029c9c3ff69456b634b4ef737b1a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---

# [!DNL Salesforce] veldtoewijzingen

De onderstaande tabellen bevatten de toewijzingen tussen [!DNL Salesforce] bronvelden en de bijbehorende XDM-velden (Experience Data Model).

## Contact {#contact}

| Bronveld | Doel XDM-veldpad | Notities |
| --- | --- | --- |
| `AccountId` | `b2b.accountKey.sourceID` |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `b2b.accountKey` |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", AccountId, "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personComponents.sourceAccountKey` |
| `"Salesforce"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `b2b.personKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `AssistantName` | `extendedWorkDetails.assistantDetails.name.fullName` |
| `AssistantPhone` | `extendedWorkDetails.assistantDetails.phone.number` |
| `Birthdate` | `person.birthDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Department` | `extendedWorkDetails.departments` |
| `Email` | `workEmail.address` | Secundaire identiteit. |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `HomePhone` | `homePhone.number` |
| `Id` | `b2b.personKey.sourceID` |
| `"Salesforce"` | `personComponents.sourcePersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `personComponents.sourcePersonKey.sourceInstanceID` |
| `Id` | `personComponents.sourcePersonKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `personComponents.sourcePersonKey.sourceKey` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastName` | `person.name.lastName` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `b2b.personSource` |
| `LeadSource` | `personComponents.personSource` |
| `MailingCity` | `workAddress.city` |
| `MailingCountry` | `workAddress.country` |
| `MailingLatitude` | `workAddress._schema.latitude` |
| `MailingLongitude` | `workAddress._schema.longitude` |
| `MailingPostalCode` | `workAddress.postalCode` |
| `MailingState` | `workAddress.state` |
| `MailingStreet` | `workAddress.street1` |
| `MobilePhone` | `mobilePhone.number` |
| `Name` | `person.name.fullName` |
| `OtherCity` | `otherAddress.city` |
| `OtherCountry` | `otherAddress.country` |
| `OtherLatitude` | `otherAddress._schema.latitude` |
| `OtherLongitude` | `otherAddress._schema.longitude` |
| `OtherPhone` | `otherPhone.number` |
| `OtherPostalCode` | `otherAddress.postalCode` |
| `OtherState` | `otherAddress.state` |
| `OtherStreet` | `otherAddress.street1` |
| `Phone` | `workPhone.number` |
| `ReportsToId` | `extendedWorkDetails.reportsToID` |
| `Salutation` | `person.name.courtesyTitle` |
| `Title` | `extendedWorkDetails.jobTitle` |

{style=&quot;table-layout:auto&quot;}

## Lood {#lead}

| Bronveld | Doel XDM-veldpad | Notities |
| --- | --- | --- |
| `City` | `workAddress.city` |
| `ConvertedContactId` | `b2b.convertedContactID` |
| `ConvertedContactId` | `personComponents.sourceConvertedContactID` |
| `ConvertedDate` | `b2b.convertedDate` |
| `Country` | `workAddress.country` |
| `Email` | `workEmail.address` | Secundaire identiteit. |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `IsConverted` | `b2b.isConverted` |
| `"Salesforce"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` |
| `Id` | `b2b.personKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `b2b.personKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `"Salesforce"` | `personComponents.sourcePersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `personComponents.sourcePersonKey.sourceInstanceID` |
| `Id` | `personComponents.sourcePersonKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `personComponents.sourcePersonKey.sourceKey` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastName` | `person.name.lastName` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `b2b.personSource` |
| `LeadSource` | `personComponents.personSource` |
| `Latitude` | `workAddress._schema.latitude` |
| `Longitude` | `workAddress._schema.longitude` |
| `MiddleName` | `person.name.middleName` |
| `Name` | `person.name.fullName` |
| `PostalCode` | `workAddress.postalCode` |
| `Salutation` | `person.name.courtesyTitle` |
| `State` | `workAddress.state` |
| `Status` | `b2b.personStatus` |
| `Status` | `personComponents.personStatus` |
| `Street` | `workAddress.street1` |
| `Title` | `extendedWorkDetails.jobTitle` |
| `Suffix` | `person.name.suffix` |
| `Company` | `b2b.companyName` |
| `Website` | `b2b.companyWebsite` |

{style=&quot;table-layout:auto&quot;}

## Account {#account}

| Bronveld | Doel XDM-veldpad | Notities |
| --- | --- | --- |
| `"Salesforce"` | `accountKey.sourceType` |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `AccountNumber` | `accountNumber` |
| `AccountSource` | `accountSourceType` |
| `AnnualRevenue` | `accountOrganization.annualRevenue.amount` |
| `BillingCity` | `accountBillingAddress.city` |
| `BillingCountry` | `accountBillingAddress.country` |
| `BillingLatitude` | `accountBillingAddress._schema.latitude` |
| `BillingLongitude` | `accountBillingAddress._schema.longitude` |
| `BillingPostalCode` | `accountBillingAddress.postalCode` |
| `BillingState` | `accountBillingAddress.state` |
| `BillingStreet` | `accountBillingAddress.street1` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `accountDescription` |
| `DunsNumber` | `accountOrganization.DUNSNumber` | data.com, functie |
| `Fax` | `accountFax.number` |
| `Id` | `accountKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `accountKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `Industry` | `accountOrganization.industry` |
| `Jigsaw` | `accountOrganization.jigsaw` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `NaicsCode` | `accountOrganization.NAICSCode` | data.com, functie |
| `NaicsDesc` | `accountOrganization.NAICSDescription` | data.com, functie |
| `Name` | `accountName` |
| `NumberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `Ownership` | `accountOwnership` |
| `ParentId` | `accountParentKey.sourceID` |
| `iif(ParentId != null && ParentId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ParentId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountParentKey` |
| `Phone` | `accountPhone.number` |
| `Rating` | `accountOrganization.rating` |
| `ShippingCity` | `accountShippingAddress.city` |
| `ShippingCountry` | `accountShippingAddress.country` |
| `ShippingLatitude` | `accountShippingAddress._schema.latitude` |
| `ShippingLongitude` | `accountShippingAddress._schema.longitude` |
| `ShippingPostalCode` | `accountShippingAddress.postalCode` |
| `ShippingState` | `accountShippingAddress.state` |
| `ShippingStreet` | `accountShippingAddress.street1` |
| `Sic` | `accountOrganization.SICCode` |
| `SicDesc` | `accountOrganization.SICDescription` |
| `Site` | `accountSite` |
| `TickerSymbol` | `accountOrganization.tickerSymbol` |
| `Tradestyle` | `accountTradeStyle` | data.com, functie |
| `Type` | `accountType` |

{style=&quot;table-layout:auto&quot;}

## Opportunity {#opportunity}

| Bronveld | Doel XDM-veldpad | Notities |
| --- | --- | --- |
| `"Salesforce"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `AccountId` | `accountKey.sourceID` |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountKey` | Relatie. |
| `Amount` | `opportunityAmount.amount` |
| `CampaignId` | `campaignKey.sourceID` |
| `iif(CampaignId != null && CampaignId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(CampaignId,"@${CRM_ORG_ID}.Salesforce")), null)` | `campaignKey` |
| `CloseDate` | `actualCloseDate` / `expectedCloseDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `opportunityDescription` |
| `ExpectedRevenue` | `expectedRevenue.amount` |
| `FiscalQuarter` | `fiscalQuarter` |
| `FiscalYear` | `fiscalYear` |
| `ForecastCategory` | `forecastCategory` |
| `ForecastCategoryName` | `forecastCategoryName` |
| `Id` | `opportunityKey.sourceID` |
| `IsClosed` | `isClosed` |
| `IsWon` | `isWon` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `leadSource` |
| `Name` | `opportunityName` |
| `NextStep` | `nextStep` |
| `Probability` | `probabilityPercentage` |
| `StageName` | `opportunityStage` |
| `TotalOpportunityQuantity` | `opportunityQuantity` |
| `Type` | `opportunityType` |

{style=&quot;table-layout:auto&quot;}

## Contactrol opportunity {#opportunity-contact-role}

| Bronveld | Doel XDM-veldpad | Notities |
| --- | --- | --- |
| `"Salesforce"` | `opportunityPersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `"Salesforce"` | `personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `personKey.sourceInstanceID` |
| `ContactId` | `personKey.sourceID` |
| `concat(ContactId,"@${CRM_ORG_ID}.Salesforce")` | `personKey.sourceKey` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Id` | `opportunityPersonKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `opportunityPersonKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `IsPrimary` | `isPrimary` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `"Salesforce"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` |
| `OpportunityId` | `opportunityKey.sourceID` |
| `concat(OpportunityId,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` |
| `Role` | `personRole` |

{style=&quot;table-layout:auto&quot;}

## Campaign {#campaign}

| Bronveld | Doel XDM-veldpad | Notities |
| --- | --- | --- |
| `"Salesforce"` | `campaignKey.sourceType` |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `Id` | `campaignKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `campaignKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `Name` | `campaignName` |
| `ParentId` | `parentCampaignKey.sourceID` |
| `iif(ParentId != null && ParentId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ParentId,"@${CRM_ORG_ID}.Salesforce")), null)` | `parentCampaignKey` |
| `Type` | `campaignType` |
| `Status` | `campaignStatus` |
| `StartDate` | `campaignStartDate` |
| `EndDate` | `campaignEndDate` |
| `ExpectedRevenue` | `expectedRevenue.amount` |
| `BudgetedCost` | `budgetedCost.amount` |
| `ActualCost` | `actualCost.amount` |
| `ExpectedResponse` | `expectedResponse` |
| `IsActive` | `isActive` |
| `Description` | `campaignDescription` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |

## Campagnelid {#campaign-member}

| Bronveld | Doel XDM-veldpad | Notities |
| --- | --- | --- |
| `"Salesforce"` | `campaignMemberKey.sourceType` |
| `"${CRM_ORG_ID}"` | `campaignMemberKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `Id` | `campaignMemberKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `campaignMemberKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `"Salesforce"` | `campaignKey.sourceType` |
| `${CRM_ORG_ID}` | `campaignKey.sourceInstanceID` |
| `CampaignId` | `campaignKey.sourceID` |
| `concat(CampaignId,"@${CRM_ORG_ID}.Salesforce")` | `campaignKey.sourceKey` |
| `"Salesforce"` | `personKey.sourceType` |
| `${CRM_ORG_ID}` | `personKey.sourceInstanceID` |
| `LeadOrContactId` | `personKey.sourceID` |
| `concat(LeadOrContactId,"@${CRM_ORG_ID}.Salesforce")` | `personKey.sourceKey` |
| `Status` | `memberStatus` |
| `HasResponded` | `hasResponded` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `FirstRespondedDate` | `firstRespondedDate` |

## Volgende stappen

Door dit document te lezen hebt u meer inzicht gekregen in de relatie tussen [!DNL Salesforce] bronvelden en de bijbehorende XDM-velden. Zie de documentatie op [een [!DNL Salesforce] bronverbinding](../../../connectors/crm/salesforce.md) voor meer informatie .
