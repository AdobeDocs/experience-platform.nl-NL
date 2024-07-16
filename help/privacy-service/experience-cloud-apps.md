---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Toepassingen voor Privacy Service en Experience Cloud
description: Dit document bevat een referentie voor het configureren van verschillende Experiencen Cloud voor bewerkingen met betrekking tot privacy.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 46ca46460de9211c3e876454c986d030b964646e
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 4%

---

# [!DNL Privacy Service] en [!DNL Experience Cloud] toepassingen

Adobe Experience Platform [!DNL Privacy Service] is ontwikkeld ter ondersteuning van privacyverzoeken voor verschillende Adobe Experience Cloud-toepassingen. Elke toepassing ondersteunt verschillende productwaarden en id&#39;s voor het identificeren van betrokkenen.

Dit document dient als referentie voor de documentatie van de [!DNL Experience Cloud] -toepassing waarin wordt beschreven hoe u die toepassing kunt configureren voor bewerkingen die betrekking hebben op privacy. Hieronder ziet u hoe u uw gegevens kunt opmaken en labelen. Er zijn twee categorieën aanvragen:

* [ Toepassingen die met Privacy Service ](#integrated) worden geïntegreerd: Toepassingen die toegang, schrapping, of opt-out verzoeken aan [!DNL Privacy Service] kunnen verzenden.
* [ Zelf-servertoepassingen ](#self-serve): De toepassingen die hun privacyverzoeken intern moeten beheren, en kunnen niet met [!DNL Privacy Service] direct communiceren.

Lees de documentatie bij uw [!DNL Experience Cloud] -toepassingen voor meer informatie over het opmaken van uw privacyverzoeken en over de waarden die worden ondersteund voor deze aanvragen.

## Toepassingen die zijn geïntegreerd met [!DNL Privacy Service] {#integrated}

Hieronder volgt een lijst met [!DNL Experience Cloud] -toepassingen die zijn geïntegreerd met [!DNL Privacy Service] , waaronder de [!DNL Privacy Service] -mogelijkheden waarmee ze compatibel zijn, hun protocollen voor het verwerken van verwijderingsaanvragen en koppelingen naar documentatie voor meer informatie.

>[!NOTE]
>
>Alle geïntegreerde producten reageren binnen 30 dagen op privacyverzoeken.

| Toepassing | Toegang/verwijderen | Uitschakelen van verkoop | Gedrag verwijderen | Documentatie en andere overwegingen |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | De cookie-id of apparaat-id van de betrokkene wordt uit het systeem verwijderd, samen met alle kosten, klik- en inkomstengegevens die bij het cookie horen. | <ul><li>[ toegang/schrappingsdocumentatie voor GDPR ](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[ toegang/schrap documentatie voor CCPA ](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[ Opt-uit-van-verkoop documentatie voor CCPA ](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics biedt hulpmiddelen voor het etiketteren van gegevens op basis van gevoeligheid en contractuele beperkingen. Etiketten zijn een belangrijke stap voor:<ol><li>Identificatie van gegevensonderwerpen.</li><li>Bepalen welke gegevens moeten worden geretourneerd als onderdeel van een toegangsverzoek.</li><li>Gegevensvelden identificeren die moeten worden verwijderd als onderdeel van een verwijderingsaanvraag.</li></ol> | <ul><li>[ Werkschema van de Privacy ](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)</li><li>[ Etikettering van Analytics ](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html)</li><li>[ Analytics uit Opt-out ](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Alle kenmerken en segmenten die zijn gekoppeld aan de Audience Manager-id die in het verzoek zijn opgenomen, worden verwijderd. Daarnaast worden de respectieve id&#39;s voor de persoon gekozen uit verdere gegevensverzameling en worden de respectievelijke id-toewijzingen verwijderd. | <ul><li>[ Toegang ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#access-data) / [ schrapt ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#delete-data) documentatie</li><li>[ Opt-out documentatie ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html#opt-out-calls)</li><li>[ Weigeren verzoeken ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests)</li></ul> |
| Adobe Campaign Classic | ✓ | ✓ | De opgeslagen gegevens van de betrokkene worden uit het systeem verwijderd. | <ul><li>[ het beheer van de Privacy ](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=nl).</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | De opgeslagen gegevens van de betrokkene worden uit het systeem verwijderd. | <ul><li>[ toegang/schrapt documentatie ](https://helpx.adobe.com/nl/campaign/kb/campaign-privacy.html)</li><li>[ Opt-out documentatie ](../segmentation/consents.md)</li></ul> |
| Klantkenmerken van de Adobe (CRS) | ✓ | N.v.t. | De kenmerken van de betrokkene worden uit het systeem verwijderd. | <ul><li>[ toegang/schrappingsdocumentatie voor GDPR ](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[ toegang/schrap documentatie voor CCPA ](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>Kenmerken van klanten kunnen geen gegevens overdragen en daarom zijn aanvragen om te weigeren niet van toepassing.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Wanneer het Experience Platform een schrappingsverzoek van Privacy Service ontvangt, verzendt het Platform bevestiging aan Privacy Service dat het verzoek is ontvangen en de beïnvloede gegevens voor schrapping duidelijk zijn gemaakt. De records worden vervolgens verwijderd uit het Data Lake- of Profile Store nadat de privacytaak is voltooid. Voordat de taak wordt voltooid, worden de gegevens via de elektronische weg verwijderd en zijn ze daarom niet toegankelijk voor een willekeurige platformservice. | <ul><li>[ toegang/schrap documentatie voor het meer van Gegevens ](../catalog/privacy.md)</li><li>[ toegang/schrap documentatie voor de Dienst van de Identiteit ](../identity-service/privacy.md)</li><li>[ toegang/schrap documentatie voor het Profiel van de Klant in real time ](../profile/privacy.md)</li><li>[!DNL Experience Platform] houdt rekening met [ opt-out verzoeken om publiekssegmenten ](../segmentation/consents.md).</li></ul> |
| Adobe Journey Optimizer | ✓ | N.v.t. | De opgeslagen gegevens van de betrokkene worden uit het systeem verwijderd. | <ul><li>[ toegang/schrapt documentatie ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/requests)</li></ul> |
| Adobe Pass-verificatie | ✓ | N.v.t. | De opgeslagen gegevens van de betrokkene worden uit het systeem verwijderd. | <ul><li>[ toegang/schrapt documentatie ](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Pass beschikt niet over de mogelijkheid om gegevens over te dragen, zodat aanvragen om niet in de handel te worden genomen niet van toepassing zijn.</li></ul> |
| Adobe Target | ✓ | N.v.t. | Alle gegevens die aan de id van de betrokkene zijn gekoppeld, worden uit het profiel van de bezoeker verwijderd. Geaggregeerde of geanonimiseerde gegevens die de individuele persoon niet identificeren of die anderszins niet gerelateerd zijn (zoals inhoudsgegevens), zijn niet van toepassing op verzoeken tot verwijderen. | <ul><li>[ toegang/schrapt documentatie ](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] beschikt niet over de mogelijkheid om gegevens over te dragen. Daarom zijn aanvragen om te weigeren van toepassing.</li></ul> |
| Marketo Engage | ✓ | N.v.t. | De opgeslagen gegevens van de betrokkene worden uit het systeem verwijderd. | <ul><li>[ toegang/schrapt documentatie ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] beschikt niet over de mogelijkheid om gegevens over te dragen. Daarom zijn aanvragen om te weigeren van toepassing.</li></ul> |

{style="table-layout:auto"}

## Zelfservertoepassingen {#self-serve}

Hieronder volgt een lijst met [!DNL Experience Cloud] -toepassingen die niet zijn geïntegreerd met [!DNL Privacy Service] en die hun privacyproblemen intern moeten beheren. Koppelingen naar de documentatie van elke toepassing worden gegeven, samen met een beschrijving van de inhoud van de documentatie.

| Toepassing | Documentatiebeschrijving |
| ------- | ----------- |
| [ Adobe Experience Manager ](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | Een overzicht van hoe een beheerder van de klantenprivacy of AEM beheerder GDPR- verzoeken kan behandelen. |
| [ Adobe Experience Manager Livefyre ](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Stappen voor het maken van GDPR toegang en schrappingsverzoeken gebruikend Livefyre. |
| [ Magento ](https://devdocs.magento.com/compliance/industry-compliance.html) | Zorg ervoor dat uw Magento&#39;s Commerce voldoen aan de vereisten van specifieke privacywetgeving. |
| [ Markeringen in Adobe Experience Platform ](../tags/ui/client-side/consent.md) | Hoe ontwikkelaars uitbreidingen en de regelbouwer kunnen gebruiken om opt-in en opt-out oplossingen te bepalen. |
| [ Workfront ](https://www.workfront.com/privacy-notice) | Leer hoe Workfront persoonlijke gegevens verzamelt en hoe een betrokkene een privacyaanvraag kan indienen via een formulier. |

{style="table-layout:auto"}
