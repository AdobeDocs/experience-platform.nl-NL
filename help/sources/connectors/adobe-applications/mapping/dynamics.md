---
title: Microsoft Dynamics-toewijzingsvelden
description: De onderstaande tabellen bevatten de toewijzingen tussen Microsoft Dynamics-bronvelden en de bijbehorende XDM-velden.
exl-id: 32f51761-5de3-4192-8f23-c1412ca12c08
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# [!DNL Microsoft Dynamics] veldtoewijzingen

De onderstaande tabellen bevatten de toewijzingen tussen [!DNL Microsoft Dynamics] bronvelden en de bijbehorende XDM-velden (Experience Data Model).

## Contactpersonen {#contacts}

| Source-veld | Doel XDM-veld | Notities |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |  |
| `address1_city` | `workAddress.city` |  |
| `address1_country` | `workAddress.country` |  |
| `address1_county` | `workAddress.stateProvince` |  |
| `address1_latitude` | `workAddress._schema.latitude` |  |
| `address1_line1` | `workAddress.street1` |  |
| `address1_line2` | `workAddress.street2` |  |
| `address1_line3` | `workAddress.street3` |  |
| `address1_longitude` | `workAddress._schema.longitude` |  |
| `address1_postalcode` | `workAddress.postalCode` |  |
| `address1_postofficebox` | `workAddress.postOfficeBox` |  |
| `address1_stateorprovince` | `workAddress.state` |  |
| `assistantname` | `extendedWorkDetails.assistantDetails.name.fullName` |  |
| `assistantphone` | `extendedWorkDetails.assistantDetails.phone.number` |  |
| `birthdate` | `person.birthDate` |  |
| `"Dynamics"` | `b2b.personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `contactid` | `b2b.personKey.sourceID` |  |
| `concat(contactid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `iif(contactid != null && contactid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", contactid, "sourceKey", concat(contactid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |  |
| `department` | `extendedWorkDetails.departments` |  |
| `fullname` | `person.name.fullName` |  |
| `suffix` | `person.name.suffix` |  |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey", concat(parentcustomerid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourceAccountKey` |  |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey",  concat(parentcustomerid, "@${CRM_ORG_ID}.Dynamics")), null)` | `b2b.accountKey` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `emailaddress1` | `workEmail.address` | Secundaire id. |
| `emailaddress2` | `personalEmail.address` |  |
| `emailaddress1` | `personComponents.workEmail.address` |  |
| `firstname` | `person.name.firstName` |  |
| `fullname` | `person.name.fullName` |  |
| `lastname` | `person.name.lastName` |  |
| `jobtitle` | `extendedWorkDetails.jobTitle` |  |
| `middlename` | `person.name.middleName` |  |
| `mobilephone` | `mobilePhone.number` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `salutation` | `person.name.courtesyTitle` |  |
| `telephone1` | `workPhone.number` |  |

{style="table-layout:auto"}

## Leads {#leads}

| Source-veld | Doel XDM-veld | Notities |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |
| `address1_city` | `workAddress.city` |
| `address1_country` | `workAddress.country` |
| `address1_county` | `workAddress.stateProvince` |
| `address1_latitude` | `workAddress._schema.latitude` |
| `address1_line1` | `workAddress.street1` |
| `address1_line2` | `workAddress.street2` |
| `address1_line3` | `workAddress.street3` |
| `address1_longitude` | `workAddress._schema.longitude` |
| `address1_postalcode` | `workAddress.postalCode` |
| `address1_postofficebox` | `workAddress.postOfficeBox` |
| `address1_stateorprovince` | `workAddress.state` |
| `telephone1` | `workPhone.number` |
| `mobilephone` | `mobilePhone.number` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `emailaddress1` | `workEmail.address` | Secundaire id |
| `emailaddress2` | `personalEmail.address` |
| `emailaddress1` | `personComponents.workEmail.address` |
| `fax` | `faxPhone.number` |
| `firstname` | `person.name.firstName` |
| `fullname` | `person.name.fullName` |
| `jobtitle` | `extendedWorkDetails.jobTitle` |
| `lastname` | `person.name.lastName` |
| `"Dynamics"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `leadid` | `b2b.personKey.sourceID` |
| `concat(leadid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `iif(leadid != null && leadid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", leadid, "sourceKey", concat(leadid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |
| `middlename` | `person.name.middleName` |
| `mobilephone` | `mobilePhone.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `salutation` | `person.name.courtesyTitle` |

{style="table-layout:auto"}

## Accounts {#accounts}

| Source-veld | Doel XDM-veld | Notities |
| --- | --- | --- |
| `"Dynamics"` | `accountKey.sourceType` |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `accountid` | `accountKey.sourceID` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `accountnumber` | `accountNumber` |
| `accountratingcode` | `accountOrganization.rating` |
| `address1_addressid` | `accountPhysicalAddress._id` |
| `address1_city` | `accountPhysicalAddress.city` |
| `address1_country` | `accountPhysicalAddress.country` |
| `address1_county` | `accountPhysicalAddress.region` |
| `address1_latitude` | `accountPhysicalAddress._schema.latitude` |
| `address1_line1` | `accountPhysicalAddress.street1` |
| `address1_line2` | `accountPhysicalAddress.street2` |
| `address1_line3` | `accountPhysicalAddress.street3` |
| `address1_longitude` | `accountPhysicalAddress._schema.longitude` |
| `address1_name` | `accountPhysicalAddress.label` |
| `address1_postalcode` | `accountPhysicalAddress.postalCode` |
| `address1_postofficebox` | `accountPhysicalAddress.postOfficeBox` |
| `address1_stateorprovince` | `accountPhysicalAddress.state` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `description` | `accountDescription` |
| `fax` | `accountFax.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `name` | `accountName` |
| `numberofemployees` | `accountOrganization.numberOfEmployees` |
| `revenue` | `accountOrganization.annualRevenue.amount` |
| `sic` | `accountOrganization.SICCode` |
| `telephone1` | `accountPhone.number` |
| `tickersymbol` | `accountOrganization.tickerSymbol` |
| `websiteurl` | `accountOrganization.website` |
| `concat(accountid,"@${CRM_ORG_ID}.Dynamics")` | `accountKey.sourceKey` |

{style="table-layout:auto"}

## Kansen {#opportunities}

| Source-veld | Doel XDM-veld | Notities |
| --- | --- | --- |
| `name` | `opportunityName` |
| `"Dynamics"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `iif(parentaccountid != null && parentaccountid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", parentaccountid, "sourceKey", concat(parentaccountid, "@${CRM_ORG_ID}.Dynamics")), null)` | `accountKey` |
| `actualclosedate` | `actualCloseDate` |
| `actualvalue` | `opportunityAmount.amount` |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `campaignKey` |
| `closeprobability` | `probabilityPercentage` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `description` | `opportunityDescription` |
| `estimatedclosedate` | `expectedCloseDate` |
| `estimatedvalue` | `expectedRevenue.amount` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `opportunityid` | `opportunityKey.sourceID` |
| `concat(opportunityid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `salesstage` | `opportunityStage` |
| `stepname` | `nextStep` |

{style="table-layout:auto"}

## Contactrollen opportunity {#opportunity-contact-roles}

| Source-veld | Doel XDM-veld | Notities |
| --- | --- | --- |
| `"Dynamics"` | `opportunityPersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `connectionid` | `opportunityPersonKey.sourceID` |
| `concat(connectionid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityPersonKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `iif(record1id != null && record1id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record1id, "sourceKey", concat(record1id,"@${CRM_ORG_ID}.Dynamics")), null)` | `opportunityKey` |
| `iif(record2id != null && record2id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record2id, "sourceKey", concat(record2id,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `connectionrole1.name` | `personRole` |
| `record1objecttypecode` | *de groep van het douanegebied van A moet als doelschema worden bepaald.* Zie de appendix sectie voor stappen op [&#x200B; hoe te om een picklist type brongebied aan een doelXDM schema &#x200B;](#picklist-type-fields) voor meer informatie in kaart te brengen. | Voor een lijst van mogelijke en waarden en etiketten voor het `record1objecttypecode` brongebied, zie dit [[!DNL Microsoft Dynamics]  document van de verbindingsentiteit &#x200B;](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record1objecttypecode-options). |
| `record2objecttypecode` | *de groep van het douanegebied van A moet als doelschema worden bepaald.* Zie de appendix sectie voor stappen op [&#x200B; hoe te om een picklist type brongebied aan een doelXDM schema &#x200B;](#picklist-type-fields) voor meer informatie in kaart te brengen. | Voor een lijst van mogelijke en waarden en etiketten voor het `record2objecttypecode` brongebied, zie dit [[!DNL Microsoft Dynamics]  document van de verbindingsentiteit &#x200B;](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record2objecttypecode-options). |

{style="table-layout:auto"}

## Campagnes {#campaigns}

| Source-veld | Doel XDM-veld | Notities |
| --- | --- | --- |
| `campaignid` | `campaignKey.sourceID` |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `concat(campaignid,"@${CRM_ORG_ID}.Dynamics")` | `campaignKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `"Dynamics"` | `campaignKey.sourceType` |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `extSourceSystemAudit.externalKey` | De `extSourceSystemAudit.externalKey` is de secundaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `modifiedby` | `extSourceSystemAudit.lastUpdatedBy` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `description` | `campaignDescription` |
| `name` | `campaignName` |
| `totalactualcost` | `actualCost.amount` |
| `budgetedcost` | `budgetedCost.amount` |
| `expectedrevenue` | `expectedRevenue.amount` |
| `actualend` | `campaignEndDate` |
| `actualstart` | `campaignStartDate` |
| `expectedresponse` | `expectedResponse` |
| `utcconversiontimezonecode` | `timeZone` |
| `utcconversiontimezonecode` | `timezoneName` |

{style="table-layout:auto"}

## Marketinglijst {#marketing-list}

| Source-veld | Doel XDM-veld | Notities |
| --- | --- | --- |
| `"Dynamics"` | `marketingListKey.sourceType` |
| `"${CRM_ORG_ID}"` | `marketingListKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `description` | `marketingListDescription` |
| `listname` | `marketingListName` |
| `listid` | `marketingListKey.sourceID` |
| `concat(listid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `createdon` | `extSourceSystemAudit.createdDate` |

{style="table-layout:auto"}

## Leden van de marketinglijst {#marketing-list-members}

| Source-veld | Doel XDM-veld | Notities |
| --- | --- | --- |
| `"Dynamics"` | `marketingListMemberKey.sourceType` |
| `"${CRM_ORG_ID}"` | `marketingListMemberKey.sourceInstanceID` | De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `iif(entityid != null && entityid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", entityid, "sourceKey", concat(entityid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `listmemberid` | `marketingListMemberKey.sourceID` |
| `concat(listmemberid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListMemberKey.sourceKey` | Primaire identiteit. De waarde voor `"${CRM_ORG_ID}"` wordt automatisch vervangen. |
| `iif(listid != null && listid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", listid, "sourceKey", concat(listid,"@${CRM_ORG_ID}.Dynamics")), null)` | `marketingListKey` |
| `createdon` | `extSourceSystemAudit.createdDate` |

{style="table-layout:auto"}

## Bijlage

De onderstaande secties bevatten aanvullende informatie die u kunt gebruiken bij het configureren van B2B-toewijzingen voor uw bron voor [!DNL Microsoft] dynamiek.

### Tekstvelden voor keuzelijst {#picklist-type-fields}

U kunt [&#x200B; berekende gebieden &#x200B;](../../../../data-prep/ui/mapping.md#calculated-fields) gebruiken om een picklist type brongebied van [!DNL Microsoft Dynamics] aan een doelXDM gebied in kaart te brengen.

Het veld `genderCode` bevat bijvoorbeeld twee opties:

| Waarde | Label |
| --- | --- |
| 1 | `male` |
| 2 | `female` |

U kunt de volgende opties gebruiken om het bronveld `genderCode` toe te wijzen aan het doelveld `person.gender` :

#### Een logische operator gebruiken

| Source-veld | Doel XDM-veld |
| --- | --- |
| `decode(genderCode, "1", "male", "2", "female", "default")` | `person.gender` |

In dit scenario komt de waarde overeen met de sleutel, als de sleutel wordt gevonden in opties, of `default` als `default` aanwezig is en de sleutel niet wordt gevonden. De waarde komt overeen met `null` als de opties `null` zijn of er geen `default` is en de toets niet wordt gevonden.

#### Een berekend veld gebruiken

| Source-veld | Doel XDM-veld |
| --- | --- |
| `iif(gendercode.equals("1"),"male",iif(gendercode.equals("2"),"female",null))` | `person.gender` |

>[!TIP]
>
>Een geneste herhaling van de bovenstaande bewerking lijkt op: `iif(condition, iif(cond1, tv1, fv1), iif(cond2, tv2, fv2))` .

Voor meer informatie is het [&#x200B; document over logische exploitanten in  [!DNL Data Prep]](../../../../data-prep/functions.md##logical-operators)
