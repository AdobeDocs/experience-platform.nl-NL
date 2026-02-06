---
title: Schemas in Real-Time Customer Data Platform B2B edition
description: Een overzicht van de rol van de schema's van het Gegevensmodel van de Ervaring (XDM) in Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# Schemas in Real-Time Customer Data Platform B2B edition

Adobe Real-Time Customer Data Platform B2B edition verstrekt verscheidene standaard [ klassen van de Gegevens van de Ervaring Model (XDM) ](../../xdm/schema/composition.md#class) die details over essentiële B2B gegevensentiteiten, zoals rekeningen, kansen, campagnes, en meer vangen. Bovendien staat Real-Time CDP B2B edition u toe om vele-aan-één verhoudingen tussen deze schema&#39;s te bepalen zodat kunnen zij aan geavanceerde segmentatiegebruikscase deelnemen.

>[!IMPORTANT]
>
>B2B-schema&#39;s zijn beschikbaar voor gebruik in Experience Platform-toepassingen (bijvoorbeeld in [ Customer Journey Analytics B2B edition ](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition) ). <br/> Nochtans, moet u toegang tot Real-Time CDP B2B edition hebben opdat (profielen in) B2B- schema&#39;s aan [ in real time het Profiel van de Klant ](../../profile/home.md) deelnemen.

De volgende standaardklassen zijn beschikbaar in Real-Time CDP B2B edition:

* [XDM Business Account](../../xdm/classes/b2b/business-account.md)
* [XDM Zakelijke account Person Relatie](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign-leden](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM Business Opportunity](../../xdm/classes/b2b/business-opportunity.md)
* [XDM Business Opportunity Person Relatie](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [Leden van XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list-members.md)

Om te begrijpen hoe schema&#39;s in uw B2B- werkschema passen, gelieve te zien [ leerprogramma van begin tot eind ](../b2b-tutorial.md).

Voor stappen op hoe te om een vele-aan-één verhouding tussen twee schema&#39;s tot stand te brengen, verwijs naar het leerprogramma op [ bepalend B2B schemaverhoudingen ](../../xdm/tutorials/relationship-b2b.md).

Als u een B2B bronverbinding gebruikt, kunt u een hulpmiddel gebruiken om de vereiste schema&#39;s en de verhoudingen tussen hen automatisch te produceren. Zie de gids op [ B2B namespaces ](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) in de brondocumentatie voor meer informatie.


De volgende tabel bevat informatie over de onderliggende opstelling van B2B-schema&#39;s.

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Schemanaam | Basisklasse | Veldgroepen | [!DNL Profile] in schema | Primaire identiteit | Primaire naamruimte | Secundaire identiteit | Secundaire naamruimte voor identiteit | Relatie | Notities |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B-account | [ XDM BedrijfsRekening ](../../xdm/classes/b2b/business-account.md) | XDM-bedrijfsaccountgegevens | Ingeschakeld | `accountKey.sourceKey` in de basisklasse | B2B-account | `extSourceSystemAudit.externalKey.sourceKey` in de basisklasse | B2B-account | <ul><li>`accountParentKey.sourceKey` in de XDM Business Account Details-veldgroep</li><li>Eigenschap van bestemming: `/accountKey/sourceKey`</li><li>Type: een-op-een</li><li>Referentieschema: B2B-account</li><li>Naamruimte: B2B-account</li></ul> |  |
| B2B-persoon | [ XDM Individueel Profiel ](../../xdm/classes/individual-profile.md) | <ul><li>XDM Business Person - Gegevens</li><li>XDM Business Person-componenten</li><li>IdentityMap</li><li>Details van goedkeuring en voorkeur</li></ul> | Ingeschakeld | `b2b.personKey.sourceKey` in de XDM Business Person Details Field Group | B2B-persoon | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` van de XDM Business Person Details-veldgroep</li><li>`workEmail.address` van de XDM Business Person Details-veldgroep</ol></li> | <ol><li>B2B-persoon</li><li>Email</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` van XDM Business Person Components, veldgroep</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-account</li><li>Naamruimte: B2B-account</li><li>Bestemmingseigenschap: accountKey.sourceKey</li><li>Relatienaam uit huidig schema: Account</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> |  |
| B2B-opportuniteit | [ XDM Business Opportunity ](../../xdm/classes/b2b/business-opportunity.md) | XDM Business Opportunity-gegevens | Ingeschakeld | `opportunityKey.sourceKey` in de basisklasse | B2B-opportuniteit | `extSourceSystemAudit.externalKey.sourceKey` in de basisklasse | B2B-opportuniteit | <ul><li>`accountKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-account</li><li>Naamruimte: B2B-account</li><li>Eigenschap van bestemming: `accountKey.sourceKey`</li><li>Relatienaam uit huidig schema: Account</li><li>Relatie naam van referentieschema: mogelijkheden</li></ul> |  |
| B2B-opportuniteitsrelatie | [ XDM de Verhouding van de Person van BedrijfsOpportunity ](../../xdm/classes/b2b/business-opportunity-person-relation.md) | Geen | Ingeschakeld | `opportunityPersonKey.sourceKey` in de basisklasse | B2B-opportuniteitsrelatie | | | **Eerste verhouding**<ul><li>`personKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-persoon</li><li>Naamruimte: B2B-persoon</li><li>Eigenschap van bestemming: b2b.personKey.sourceKey</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatie naam van referentieschema: mogelijkheden</li></ul>**Tweede verhouding**<ul><li>`opportunityKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B Opportunity </li><li>Namespace: B2B Opportunity </li><li>Eigenschap van bestemming: `opportunityKey.sourceKey`</li><li>Relatienaam uit huidig schema: Opportunity</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> |  |
| B2B-campagne | [ XDM Bedrijfs Campagne ](../../xdm/classes/b2b/business-campaign.md) | XDM Business Campaign - details | Ingeschakeld | `campaignKey.sourceKey` in de basisklasse | B2B-campagne | | | | |
| B2B Campagne-lid | [ XDM Bedrijfs Campagne Leden ](../../xdm/classes/b2b/business-campaign-members.md) | XDM Business Campagne Member Details | Ingeschakeld | `ccampaignMemberKey.sourceKey` in de basisklasse | B2B Campagne-lid | | | **Eerste verhouding**<ul><li>`personKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-persoon</li><li>Naamruimte: B2B-persoon</li><li>Eigenschap van bestemming: `b2b.personKey.sourceKey`</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatie-naam vanuit referentieschema: campagnes</li></ul>**Tweede verhouding**<ul><li>`campaignKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-campagne</li><li>Naamruimte: B2B-campagne</li><li>Eigenschap van bestemming: `campaignKey.sourceKey`</li><li>Relatienaam van huidig schema: Campagne</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> |  |
| B2B-marketinglijst | [ XDM Business Marketing List ](../../xdm/classes/b2b/business-marketing-list.md) | Geen | Ingeschakeld | `marketingListKey.sourceKey` in de basisklasse | B2B-marketinglijst | Geen | Geen | Geen | Statische lijst wordt niet gesynchroniseerd vanuit [!DNL Salesforce] en heeft daarom geen secundaire identiteit. |
| B2B Marketing List Member | [ XDM Bedrijfs de Leden van de Lijst van de Marketing ](../../xdm/classes/b2b/business-marketing-list-members.md) | Geen | Ingeschakeld | `marketingListMemberKey.sourceKey` in de basisklasse | B2B Marketing List Member | Geen | Geen | **Eerste verhouding**<ul><li>`PersonKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-persoon</li><li>Naamruimte: B2B-persoon</li><li>Eigenschap van bestemming: `b2b.personKey.sourceKey`</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatienaam van referentieschema: marketinglijsten</li></ul>**Tweede verhouding**<ul><li>`marketingListKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-marketinglijst</li><li>Naamruimte: B2B-marketinglijst</li><li>Eigenschap van bestemming: `marketingListKey.sourceKey`</li><li>Relatienaam uit huidig schema: Marketinglijst</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> | Lid van een statische lijst wordt niet gesynchroniseerd vanuit [!DNL Salesforce] en heeft daarom geen secundaire identiteit. |
| B2B Betrekking van rekeningpersoon | [ XDM de Verhouding van de Persoon van de Bedrijfs Rekening ](../../xdm/classes/b2b/business-account-person-relation.md) | Identiteitskaart | Ingeschakeld | `accountPersonKey.sourceKey` in de basisklasse | B2B Betrekking van rekeningpersoon | Geen | Geen | **Eerste verhouding**<ul><li>`personKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-persoon</li><li>Naamruimte: B2B-persoon</li><li>Eigenschap van bestemming: `b2b.personKey.SourceKey`</li><li>Relatie-naam uit huidig schema: Personen</li><li>Relatie-naam vanuit referentieschema: Account</li></ul>**Tweede verhouding**<ul><li>`accountKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-account</li><li>Naamruimte: B2B-account</li><li>Eigenschap van bestemming: `accountKey.sourceKey`</li><li>Relatienaam uit huidig schema: Account</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> |  |

{style="table-layout:auto"}

