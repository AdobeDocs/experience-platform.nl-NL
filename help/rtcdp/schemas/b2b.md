---
title: Schemas in Real-Time Customer Data Platform B2B edition
description: Een overzicht van de rol van de schema's van het Gegevensmodel van de Ervaring (XDM) in Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 0191fc8419c696d8cd114a5eb575b8cc0a815a72
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# Schemas in Real-Time Customer Data Platform B2B edition

Adobe Real-Time Customer Data Platform B2B edition verstrekt verscheidene standaard [&#x200B; klassen van de Gegevens van de Ervaring Model (XDM) &#x200B;](../../xdm/schema/composition.md#class) die details over essentiële B2B gegevensentiteiten, zoals rekeningen, kansen, campagnes, en meer vangen. Bovendien staat Real-Time CDP B2B edition u toe om vele-aan-één verhoudingen tussen deze schema&#39;s te bepalen zodat kunnen zij aan geavanceerde segmentatiegebruikscase deelnemen.

>[!IMPORTANT]
>
>B2B-schema&#39;s zijn beschikbaar voor gebruik in Experience Platform-toepassingen (bijvoorbeeld in [&#x200B; Customer Journey Analytics B2B edition &#x200B;](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition) ). <br/> Nochtans, moet u toegang tot Real-Time CDP B2B edition hebben opdat (profielen in) B2B- schema&#39;s aan [&#x200B; in real time het Profiel van de Klant &#x200B;](../../profile/home.md) deelnemen.

De volgende standaardklassen zijn beschikbaar in Real-Time CDP B2B edition:

* [XDM Business Account](../../xdm/classes/b2b/business-account.md)
* [XDM Zakelijke account Person Relatie](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign-leden](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM Business Opportunity](../../xdm/classes/b2b/business-opportunity.md)
* [XDM Business Opportunity Person Relatie](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [Leden van XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list-members.md)

Om te begrijpen hoe schema&#39;s in uw B2B- werkschema passen, gelieve te zien [&#x200B; leerprogramma van begin tot eind &#x200B;](../b2b-tutorial.md).

Voor stappen op hoe te om een vele-aan-één verhouding tussen twee schema&#39;s tot stand te brengen, verwijs naar het leerprogramma op [&#x200B; bepalend B2B schemaverhoudingen &#x200B;](../../xdm/tutorials/relationship-b2b.md).

Als u een B2B bronverbinding gebruikt, kunt u een hulpmiddel gebruiken om de vereiste schema&#39;s en de verhoudingen tussen hen automatisch te produceren. Zie de gids op [&#x200B; B2B namespaces &#x200B;](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) in de brondocumentatie voor meer informatie.


De volgende tabel bevat informatie over de onderliggende opstelling van B2B-schema&#39;s.

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Schemanaam | Basisklasse | Veldgroepen | [!DNL Profile] in schema | Primaire identiteit | Primaire naamruimte | Secundaire identiteit | Secundaire naamruimte voor identiteit | Relatie | Notities |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B-account | [&#x200B; XDM BedrijfsRekening &#x200B;](../../xdm/classes/b2b/business-account.md) | XDM-bedrijfsaccountgegevens | Ingeschakeld | `accountKey.sourceKey` in de basisklasse | B2B-account | `extSourceSystemAudit.externalKey.sourceKey` in de basisklasse | B2B-account | <ul><li>`accountParentKey.sourceKey` in de XDM Business Account Details-veldgroep</li><li>Eigenschap van bestemming: `/accountKey/sourceKey`</li><li>Type: een-op-een</li><li>Referentieschema: B2B-account</li><li>Naamruimte: B2B-account</li></ul> |
| B2B-persoon | [&#x200B; XDM Individueel Profiel &#x200B;](../../xdm/classes/individual-profile.md) | <ul><li>XDM Business Person - Gegevens</li><li>XDM Business Person-componenten</li><li>IdentityMap</li><li>Details van goedkeuring en voorkeur</li></ul> | Ingeschakeld | `b2b.personKey.sourceKey` in de XDM Business Person Details Field Group | B2B-persoon | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` van de XDM Business Person Details-veldgroep</li><li>`workEmail.address` van de XDM Business Person Details-veldgroep</ol></li> | <ol><li>B2B-persoon</li><li>Email</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` van XDM Business Person Components, veldgroep</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-account</li><li>Naamruimte: B2B-account</li><li>Bestemmingseigenschap: accountKey.sourceKey</li><li>Relatienaam uit huidig schema: Account</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> |
| B2B-opportuniteit | [&#x200B; XDM Business Opportunity &#x200B;](../../xdm/classes/b2b/business-opportunity.md) | XDM Business Opportunity-gegevens | Ingeschakeld | `opportunityKey.sourceKey` in de basisklasse | B2B-opportuniteit | `extSourceSystemAudit.externalKey.sourceKey` in de basisklasse | B2B-opportuniteit | <ul><li>`accountKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-account</li><li>Naamruimte: B2B-account</li><li>Eigenschap van bestemming: `accountKey.sourceKey`</li><li>Relatienaam uit huidig schema: Account</li><li>Relatie naam van referentieschema: mogelijkheden</li></ul> |
| B2B-opportuniteitsrelatie | [&#x200B; XDM de Verhouding van de Person van BedrijfsOpportunity &#x200B;](../../xdm/classes/b2b/business-opportunity-person-relation.md) | Geen | Ingeschakeld | `opportunityPersonKey.sourceKey` in de basisklasse | B2B-opportuniteitsrelatie | | | **Eerste verhouding**<ul><li>`personKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-persoon</li><li>Naamruimte: B2B-persoon</li><li>Eigenschap van bestemming: b2b.personKey.sourceKey</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatie naam van referentieschema: mogelijkheden</li></ul>**Tweede verhouding**<ul><li>`opportunityKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B Opportunity </li><li>Namespace: B2B Opportunity </li><li>Eigenschap van bestemming: `opportunityKey.sourceKey`</li><li>Relatienaam uit huidig schema: Opportunity</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> |
| B2B-campagne | [&#x200B; XDM Bedrijfs Campagne &#x200B;](../../xdm/classes/b2b/business-campaign.md) | XDM Business Campaign - details | Ingeschakeld | `campaignKey.sourceKey` in de basisklasse | B2B-campagne | | |
| B2B Campagne-lid | [&#x200B; XDM Bedrijfs Campagne Leden &#x200B;](../../xdm/classes/b2b/business-campaign-members.md) | XDM Business Campagne Member Details | Ingeschakeld | `ccampaignMemberKey.sourceKey` in de basisklasse | B2B Campagne-lid | | | **Eerste verhouding**<ul><li>`personKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-persoon</li><li>Naamruimte: B2B-persoon</li><li>Eigenschap van bestemming: `b2b.personKey.sourceKey`</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatie-naam vanuit referentieschema: campagnes</li></ul>**Tweede verhouding**<ul><li>`campaignKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-campagne</li><li>Naamruimte: B2B-campagne</li><li>Eigenschap van bestemming: `campaignKey.sourceKey`</li><li>Relatienaam van huidig schema: Campagne</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> |
| B2B-marketinglijst | [&#x200B; XDM Business Marketing List &#x200B;](../../xdm/classes/b2b/business-marketing-list.md) | Geen | Ingeschakeld | `marketingListKey.sourceKey` in de basisklasse | B2B-marketinglijst | Geen | Geen | Geen | Statische lijst wordt niet gesynchroniseerd vanuit [!DNL Salesforce] en heeft daarom geen secundaire identiteit. |
| B2B Marketing List Member | [&#x200B; XDM Bedrijfs de Leden van de Lijst van de Marketing &#x200B;](../../xdm/classes/b2b/business-marketing-list-members.md) | Geen | Ingeschakeld | `marketingListMemberKey.sourceKey` in de basisklasse | B2B Marketing List Member | Geen | Geen | **Eerste verhouding**<ul><li>`PersonKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-persoon</li><li>Naamruimte: B2B-persoon</li><li>Eigenschap van bestemming: `b2b.personKey.sourceKey`</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatienaam van referentieschema: marketinglijsten</li></ul>**Tweede verhouding**<ul><li>`marketingListKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-marketinglijst</li><li>Naamruimte: B2B-marketinglijst</li><li>Eigenschap van bestemming: `marketingListKey.sourceKey`</li><li>Relatienaam uit huidig schema: Marketinglijst</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> | Lid van een statische lijst wordt niet gesynchroniseerd vanuit [!DNL Salesforce] en heeft daarom geen secundaire identiteit. |
| B2B Betrekking van rekeningpersoon | [&#x200B; XDM de Verhouding van de Persoon van de Bedrijfs Rekening &#x200B;](../../xdm/classes/b2b/business-account-person-relation.md) | Identiteitskaart | Ingeschakeld | `accountPersonKey.sourceKey` in de basisklasse | B2B Betrekking van rekeningpersoon | Geen | Geen | **Eerste verhouding**<ul><li>`personKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-persoon</li><li>Naamruimte: B2B-persoon</li><li>Eigenschap van bestemming: `b2b.personKey.SourceKey`</li><li>Relatie-naam uit huidig schema: Personen</li><li>Relatie-naam vanuit referentieschema: Account</li></ul>**Tweede verhouding**<ul><li>`accountKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-account</li><li>Naamruimte: B2B-account</li><li>Eigenschap van bestemming: `accountKey.sourceKey`</li><li>Relatienaam uit huidig schema: Account</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> |

{style="table-layout:auto"}

