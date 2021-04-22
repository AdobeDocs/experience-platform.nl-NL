---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Privacy Service- en Experience Cloud-toepassingen
topic-legacy: overview
description: Dit document bevat een referentie voor het configureren van verschillende Experience Cloud-toepassingen voor bewerkingen met betrekking tot privacy.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
translation-type: tm+mt
source-git-commit: e226990fc84926587308077b32b128bfe334e812
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Privacy Service] en  [!DNL Experience Cloud] toepassingen

Adobe Experience Platform [!DNL Privacy Service] is ontwikkeld ter ondersteuning van privacyverzoeken voor verschillende Adobe Experience Cloud-toepassingen. Elke toepassing ondersteunt verschillende productwaarden en id&#39;s voor het identificeren van betrokkenen.

Dit document dient als referentie voor toepassingsdocumentatie [!DNL Experience Cloud] die schetst hoe te om die toepassing voor op privacy betrekking hebbende verrichtingen te vormen. Hieronder ziet u hoe u uw gegevens kunt opmaken en labelen. Er zijn twee categorieën aanvragen:

* [Toepassingen die zijn geïntegreerd met Privacy Service](#integrated): Toepassingen die toegang kunnen verzenden, aanvragen kunnen verwijderen of weigeren aan  [!DNL Privacy Service].
* [Zelfservertoepassingen](#self-serve): Toepassingen die hun privacyverzoeken intern moeten beheren en niet  [!DNL Privacy Service] rechtstreeks kunnen communiceren.

Raadpleeg de documentatie bij uw [!DNL Experience Cloud]-toepassingen voor meer informatie over het opmaken van uw privacyverzoeken en over de waarden die worden ondersteund voor deze aanvragen.

## Toepassingen die zijn geïntegreerd met [!DNL Privacy Service] {#integrated}

Hieronder volgt een lijst met [!DNL Experience Cloud] toepassingen die zijn geïntegreerd met [!DNL Privacy Service], inclusief de [!DNL Privacy Service] mogelijkheden waarmee deze compatibel zijn, en koppelingen naar documentatie voor meer informatie.

| Toepassing | Toegang/verwijderen | Uitschakelen van verkoop | Documentatie en overwegingen |
| --- | :---: | :---: | --- |
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Toegang tot/verwijder documentatie voor GDPR](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Toegang/schrappingsdocumentatie voor CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Opt-out-of-sales documentatie voor CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Documentatie openen/verwijderen](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] behandelt opt-out verzoeken door  [privacy rapporteringsvariabelen te gebruiken](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Documentatie openen/verwijderen](https://docs.adobe.com/content/help/en/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentatie bij uitsluiting](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Documentatie openen/verwijderen](https://helpx.adobe.com/nl/campaign/kb/campaign-privacy.html)</li><li>[Documentatie bij uitsluiting](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe Klantenattributen (CRS) | ✓ | N.v.t. | <ul><li>[Toegang tot/verwijder documentatie voor GDPR](https://docs.adobe.com/content/help/nl-NL/core-services/interface/customer-attributes/gdpr.html)</li><li>[Toegang/schrappingsdocumentatie voor CCPA](https://docs.adobe.com/content/help/nl-NL/core-services/interface/customer-attributes/ccpa.html)</li><li>Kenmerken van klanten kunnen geen gegevens overdragen en daarom zijn aanvragen om te weigeren niet van toepassing.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Toegang tot/verwijdering van documentatie voor het Data Lake](../catalog/privacy.md)</li><li>[Documentatie voor realtime-klantprofiel openen/verwijderen](../profile/privacy.md)</li><li>[!DNL Experience Platform] geeft gehoor aan  [opt-outverzoeken voor publiekssegmenten](../segmentation/honoring-opt-outs.md).</li></ul> |
| Adobe Primetime-verificatie | ✓ | N.v.t. | <ul><li>[Documentatie openen/verwijderen](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] niet over de mogelijkheid beschikt om gegevens over te dragen, zodat verzoeken om niet in aanmerking te komen voor verkoop niet van toepassing zijn.</li></ul> |
| Adobe Target | ✓ | N.v.t. | <ul><li>[Documentatie openen/verwijderen](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] niet over de mogelijkheid beschikt om gegevens over te dragen, zodat verzoeken om niet in aanmerking te komen voor verkoop niet van toepassing zijn.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Zelfservertoepassingen {#self-serve}

Hieronder volgt een lijst met [!DNL Experience Cloud]-toepassingen die niet zijn geïntegreerd met [!DNL Privacy Service] en die hun privacyproblemen intern moeten beheren. Koppelingen naar de documentatie van elke toepassing worden gegeven, samen met een beschrijving van de inhoud van de documentatie.

| Toepassing | Documentatiebeschrijving |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/ACC_GDPR.html) | Een overzicht van GDPR-functies voor Adobe Campaign Classic. |
| [Adobe dynamisch tagbeheer](https://docs.adobe.com/content/help/nl-NL/dtm/using/tools/opt-in.html) | Stappen om te voorkomen dat de Adobe-tags worden ontstoken totdat de toestemming is verkregen. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Een overzicht van hoe een beheerder van de klantenprivacy of AEM beheerder GDPR- verzoeken kan behandelen. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Stappen voor het maken van GDPR toegang en schrapping verzoeken gebruikend Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Hoe ontwikkelaars uitbreidingen en de regelbouwer kunnen gebruiken om opt-in en opt-out oplossingen te bepalen. |

{style=&quot;table-layout:auto&quot;}
