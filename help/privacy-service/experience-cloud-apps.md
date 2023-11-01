---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Toepassingen voor Privacy Service en Experience Cloud
description: Dit document bevat een referentie voor het configureren van verschillende Experiencen Cloud voor bewerkingen met betrekking tot privacy.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 7%

---

# [!DNL Privacy Service] en [!DNL Experience Cloud] toepassingen

Adobe Experience Platform [!DNL Privacy Service] is ontwikkeld ter ondersteuning van privacyverzoeken voor verschillende Adobe Experience Cloud-toepassingen. Elke toepassing ondersteunt verschillende productwaarden en id&#39;s voor het identificeren van betrokkenen.

Dit document dient als referentie voor [!DNL Experience Cloud] toepassingsdocumentatie die schetst hoe te om die toepassing voor op privacy betrekking hebbende verrichtingen te vormen. Hieronder ziet u hoe u uw gegevens kunt opmaken en labelen. Er zijn twee categorieën aanvragen:

* [Toepassingen die zijn geïntegreerd met Privacy Service](#integrated): Toepassingen die toegang kunnen verzenden, aanvragen kunnen verwijderen of weigeren aan [!DNL Privacy Service].
* [Zelfservertoepassingen](#self-serve): Toepassingen die hun privacyverzoeken intern moeten beheren en niet kunnen communiceren met [!DNL Privacy Service] rechtstreeks.

Lees de documentatie voor uw [!DNL Experience Cloud] toepassingen om te leren hoe u uw privacyverzoeken kunt opmaken en welke waarden worden ondersteund voor deze aanvragen.

## Toepassingen geïntegreerd met [!DNL Privacy Service] {#integrated}

Hieronder volgt een lijst met [!DNL Experience Cloud] toepassingen die zijn geïntegreerd met [!DNL Privacy Service], met inbegrip van [!DNL Privacy Service] de mogelijkheden zij met, hun protocollen voor verwerking schrappingsverzoeken, en verbindingen aan documentatie voor meer informatie compatibel zijn.

>[!NOTE]
>
>Alle geïntegreerde producten reageren binnen 30 dagen op privacyverzoeken.

| Toepassing | Toegang/verwijderen | Uitschakelen van verkoop | Gedrag verwijderen | Documentatie en andere overwegingen |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | De cookie-id of apparaat-id van de betrokkene wordt uit het systeem verwijderd, samen met alle kosten, klik- en inkomstengegevens die bij het cookie horen. | <ul><li>[Toegang tot/verwijder documentatie voor GDPR](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Toegang/schrappingsdocumentatie voor CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Opt-out-of-sales documentatie voor CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics biedt tools voor het labelen van data op basis van de gevoeligheid en contractuele beperkingen ervan. Etiketten zijn een belangrijke stap voor:<ol><li>Identificatie van gegevensonderwerpen.</li><li>Bepalen welke gegevens moeten worden geretourneerd als onderdeel van een toegangsverzoek.</li><li>Gegevensvelden identificeren die moeten worden verwijderd als onderdeel van een verwijderingsaanvraag.</li></ol> | <ul><li>[Privacy Workflow](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)</li><li>[Labels voor Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html)</li><li>[Analyse bij voorkeur uit](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Alle kenmerken en segmenten die zijn gekoppeld aan de Audience Manager-id die in het verzoek zijn opgenomen, worden verwijderd. Daarnaast worden de respectieve id&#39;s voor de persoon gekozen uit verdere gegevensverzameling en worden de respectievelijke id-toewijzingen verwijderd. | <ul><li>[Toegang](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#access-data) / [delete](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#delete-data) documentatie</li><li>[Documentatie bij uitsluiting](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html#opt-out-calls)</li><li>[Afmelden](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | De opgeslagen gegevens van de betrokkene worden uit het systeem verwijderd. | <ul><li>[Documentatie openen/verwijderen](https://helpx.adobe.com/nl/campaign/kb/campaign-privacy.html)</li><li>[Documentatie bij uitsluiting](../segmentation/consents.md)</li></ul> |
| Klantkenmerken van de Adobe (CRS) | ✓ | N.v.t. | De kenmerken van de betrokkene worden uit het systeem verwijderd. | <ul><li>[Toegang tot/verwijder documentatie voor GDPR](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[Toegang/schrappingsdocumentatie voor CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>Kenmerken van klanten kunnen geen gegevens overdragen en daarom zijn aanvragen om te weigeren niet van toepassing.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Wanneer het Experience Platform een schrappingsverzoek van Privacy Service ontvangt, verzendt het Platform bevestiging aan Privacy Service dat het verzoek is ontvangen en de beïnvloede gegevens voor schrapping duidelijk zijn gemaakt. De records worden vervolgens verwijderd uit het Data Lake- of Profile Store nadat de privacytaak is voltooid. Voordat de taak wordt voltooid, worden de gegevens via de elektronische weg verwijderd en zijn ze daarom niet toegankelijk voor een willekeurige platformservice. | <ul><li>[Toegang tot/verwijdering van documentatie voor het Data Lake](../catalog/privacy.md)</li><li>[Documentatie voor toegang/verwijdering voor identiteitsservice](../identity-service/privacy.md)</li><li>[Documentatie voor realtime-klantprofiel openen/verwijderen](../profile/privacy.md)</li><li>[!DNL Experience Platform] eer [opt-out-aanvragen voor publiekssegmenten](../segmentation/consents.md).</li></ul> |
| Adobe Pass-verificatie | ✓ | N.v.t. | De opgeslagen gegevens van de betrokkene worden uit het systeem verwijderd. | <ul><li>[Documentatie openen/verwijderen](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Pass beschikt niet over de mogelijkheid om gegevens over te dragen, zodat aanvragen om niet in de handel te worden genomen niet van toepassing zijn.</li></ul> |
| Adobe Target | ✓ | N.v.t. | Alle gegevens die aan de id van de betrokkene zijn gekoppeld, worden uit het profiel van de bezoeker verwijderd. Geaggregeerde of geanonimiseerde gegevens die de individuele persoon niet identificeren of die anderszins niet gerelateerd zijn (zoals inhoudsgegevens), zijn niet van toepassing op verzoeken tot verwijderen. | <ul><li>[Documentatie openen/verwijderen](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] niet over de mogelijkheid beschikt om gegevens over te dragen, zodat verzoeken om niet in aanmerking te komen voor verkoop niet van toepassing zijn.</li></ul> |
| Marketo Engage | ✓ | N.v.t. | De opgeslagen gegevens van de betrokkene worden uit het systeem verwijderd. | <ul><li>[Documentatie openen/verwijderen](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] niet over de mogelijkheid beschikt om gegevens over te dragen, zodat verzoeken om niet in aanmerking te komen voor verkoop niet van toepassing zijn.</li></ul> |

{style="table-layout:auto"}

## Zelfservertoepassingen {#self-serve}

Hieronder volgt een lijst met [!DNL Experience Cloud] toepassingen die niet zijn geïntegreerd met [!DNL Privacy Service] en moeten hun privacyproblemen intern aanpakken. Koppelingen naar de documentatie van elke toepassing worden gegeven, samen met een beschrijving van de inhoud van de documentatie.

| Toepassing | Documentatiebeschrijving |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=nl) | Een overzicht van de GDPR-functies voor Adobe Campaign Classic. |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | Een overzicht van hoe een beheerder van de klantenprivacy of AEM beheerder GDPR- verzoeken kan behandelen. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Stappen voor het maken van GDPR toegang en schrappingsverzoeken gebruikend Livefyre. |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | Zorg ervoor dat uw Magento&#39;s Commerce voldoen aan de vereisten van specifieke privacywetgeving. |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | Leer hoe privacyregels gelden voor Marketo. |
| [Tags in Adobe Experience Platform](../tags/ui/client-side/consent.md) | Hoe ontwikkelaars uitbreidingen en de regelbouwer kunnen gebruiken om opt-in en opt-out oplossingen te bepalen. |
| [Workfront](https://www.workfront.com/privacy-notice) | Leer hoe Workfront persoonlijke gegevens verzamelt en hoe een betrokkene een privacyaanvraag kan indienen via een formulier. |

{style="table-layout:auto"}
