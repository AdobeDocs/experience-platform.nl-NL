---
title: Salesforce-toewijzingsvelden
description: De onderstaande tabellen bevatten de toewijzingen tussen Salesforce-bronvelden en de bijbehorende XDM-velden.
exl-id: 33ee76f2-0495-4acd-a862-c942c0fa3177
source-git-commit: ec42cf27c082611acb1a08500b7bbd23fc34d730
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# [!DNL Salesforce] veldtoewijzingen

De onderstaande tabellen bevatten de toewijzingen tussen [!DNL Salesforce] bronvelden en de bijbehorende XDM-velden (Experience Data Model).

## Contact {#contact}

Lees het [&#x200B; XDM Individuele overzicht van het Profiel &#x200B;](../../../../xdm/classes/individual-profile.md) voor meer informatie over de klasse XDM. Voor meer informatie over de XDM gebiedsgroepen, lees de [&#128279;](../../../../xdm/field-groups/profile/business-person-details.md) gids van de het schemagroep van de Details van de BedrijfsPersoon van 0&rbrace; XDM &lbrace;en [&#x200B; XDM van de BedrijfsPersoon de het schemagroep van Componenten van de Componenten &#x200B;](../../../../xdm/field-groups/profile/business-person-components.md).

| Source-veld | Doel XDM-veldpad | Notities |
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
| `Email` | `workEmail.address` | Secundaire identiteit |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `HomePhone` | `homePhone.number` |
| `isDeleted` | `isDeleted` |
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
| `"Contact"` | `b2b.personType` |

{style="table-layout:auto"}

## Lood {#lead}

Lees het [&#x200B; XDM Individuele overzicht van het Profiel &#x200B;](../../../../xdm/classes/individual-profile.md) voor meer informatie over de klasse XDM. Voor meer informatie over de XDM gebiedsgroepen, lees de [&#128279;](../../../../xdm/field-groups/profile/business-person-details.md) gids van de het schemagroep van de Details van de BedrijfsPersoon van 0&rbrace; XDM &lbrace;en [&#x200B; XDM van de BedrijfsPersoon de het schemagroep van Componenten van de Componenten &#x200B;](../../../../xdm/field-groups/profile/business-person-components.md).

| Source-veld | Doel XDM-veldpad | Notities |
| --- | --- | --- |
| `City` | `workAddress.city` |
| `ConvertedDate` | `b2b.convertedDate` |
| `Country` | `workAddress.country` |
| `Email` | `workEmail.address` | Secundaire identiteit |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `IsConverted` | `b2b.isConverted` |
| `isDeleted` | `isDeleted` |
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
| `ConvertedContactId` | `b2b.convertedContactKey.sourceID` |
| `iif(ConvertedContactId != null && ConvertedContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ConvertedContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `b2b.convertedContactKey` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `"Lead"` | `b2b.personType` |
| `iif(ConvertedContactId != null && ConvertedContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", ConvertedContactId, "sourceKey", concat(ConvertedContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personComponents.sourceConvertedContactKey` |

{style="table-layout:auto"}

## Account {#account}

Lees het [&#x200B; XDM overzicht van de details van de BedrijfsRekening &#x200B;](../../../../xdm/classes/b2b/business-account.md) voor meer informatie over de klasse XDM.

| Source-veld | Doel XDM-veldpad | Notities |
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
| `isDeleted` | `isDeleted` |
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
| `Website` | `accountOrganization.website` |

{style="table-layout:auto"}

## Opportunity {#opportunity}

Lees het [&#x200B; XDM overzicht van de BedrijfsKans &#x200B;](../../../../xdm/classes/b2b/business-opportunity.md) voor meer informatie over de klasse XDM.

| Source-veld | Doel XDM-veldpad | Notities |
| --- | --- | --- |
| `"Salesforce"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `AccountId` | `accountKey.sourceID` |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountKey` | Relatie. |
| `Amount` | `opportunityAmount.amount` |
| `CampaignId` | `campaignKey.sourceID` |
| `iif(CampaignId != null && CampaignId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(CampaignId,"@${CRM_ORG_ID}.Salesforce")), null)` | `campaignKey` |
| `CloseDate` | `expectedCloseDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `opportunityDescription` |
| `ExpectedRevenue` | `expectedRevenue.amount` |
| `FiscalQuarter` | `fiscalQuarter` |
| `FiscalYear` | `fiscalYear` |
| `ForecastCategory` | `forecastCategory` |
| `ForecastCategoryName` | `forecastCategoryName` |
| `Id` | `opportunityKey.sourceID` |
| `IsClosed` | `isClosed` |
| `isDeleted` | `isDeleted` |
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
| `CurrencyIsoCode` | `opportunityAmount.currencyCode` |

{style="table-layout:auto"}

## Contactrol opportunity {#opportunity-contact-role}

Lees [&#x200B; XDM de klassenoverzicht van de Verhouding van de Onderneming van de Opportunity &#x200B;](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) voor meer informatie over de klasse XDM.

| Source-veld | Doel XDM-veldpad | Notities |
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
| `isDeleted` | `isDeleted` |
| `IsPrimary` | `isPrimary` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `"Salesforce"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` |
| `OpportunityId` | `opportunityKey.sourceID` |
| `concat(OpportunityId,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` |
| `Role` | `personRole` |

{style="table-layout:auto"}

## Campaign {#campaign}

Lees het [&#x200B; XDM BedrijfsCampagne klassenoverzicht &#x200B;](../../../../xdm/classes/b2b/business-campaign.md) voor meer informatie over de klasse XDM. Voor meer informatie over de XDM gebiedsgroepen, lees de [&#128279;](../../../../xdm/field-groups/b2b-campaign/details.md) gids van het de detailsschema van de BedrijfsCampagne van de 0&rbrace; XDM van de de detailhandel van de Campagne groep &lbrace;.

| Source-veld | Doel XDM-veldpad | Notities |
| --- | --- | --- |
| `"Salesforce"` | `campaignKey.sourceType` |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `isDeleted` | `isDeleted` |
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
| `CurrencyIsoCode` | `actualCost.currencyCode` |

## Campagnelid {#campaign-member}

Lees het [&#x200B; XDM overzicht van de Leden Bedrijfs van de Campagne &#x200B;](../../../../xdm/classes/b2b/business-campaign-members.md) voor meer informatie over de klasse XDM. Voor meer informatie over de XDM gebiedsgroepen, lees het [&#x200B; XDM Van Bedrijfs het detailsschemagebied van het Lid van de Campagne &#x200B;](../../../../xdm/field-groups/b2b-campaign/details.md) document.

| Source-veld | Doel XDM-veldpad | Notities |
| --- | --- | --- |
| `"Salesforce"` | `campaignMemberKey.sourceType` |
| `"${CRM_ORG_ID}"` | `campaignMemberKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `isDeleted` | `isDeleted` |
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
| `Type` | `b2b.personType` |

## Contactpersoon account {#account-contact-relation}

Lees de [&#x200B; klasse van de Verhouding van de Person van de BedrijfsRekening XDM &#x200B;](../../../../xdm/classes/b2b/business-account-person-relation.md) voor meer informatie over de klasse XDM.

| Source-veld | Doel XDM-veldpad | Notities |
| --- | --- | --- |
| `AccountId` | `accountKey.sourceID` |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountKey` |
| `ContactId` | `personKey.sourceID` |
| `iif(ContactId != null && ContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personKey` |
| `CreatedById` | `extSourceSystemAudit.createdBy` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `EndDate` | `relationEndDate` |
| `IsDeleted` | `isDeleted` |
| `Id` | `accountPersonKey.sourceID` |
| `"Salesforce"` | `accountPersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `accountPersonKey.sourceInstanceID` |
| `concat(Id, "@${CRM_ORG_ID}.Salesforce")` | `accountPersonKey.sourceKey` | Primaire identiteit. |
| `IsActive` | `IsActive` |
| `IsDirect` | `IsDirect` |
| `LastModifiedById` | `extSourceSystemAudit.lastUpdatedBy` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `explode(Roles,";")` | `personRoles[]` |
| `StartDate` | `relationStartDate` |

## Volgende stappen

Door dit document te lezen, hebt u meer inzicht gekregen in de toewijzingsrelatie tussen [!DNL Salesforce] bronvelden en de bijbehorende XDM-velden. Zie de documentatie bij [&#x200B; het creëren van a  [!DNL Salesforce]  bronverbinding &#x200B;](../../../connectors/crm/salesforce.md) voor meer informatie.
