---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service en Experience Cloud-toepassingen
topic: overview
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Privacy Service en Experience Cloud-toepassingen

De Adobe Experience Platform Privacy Service is ontwikkeld ter ondersteuning van privacyverzoeken voor verschillende Adobe Experience Cloud-toepassingen. Elke toepassing ondersteunt verschillende productwaarden en id&#39;s voor het identificeren van betrokkenen.

Dit document fungeert als referentie voor de toepassingsdocumentatie van Experience Cloud waarin wordt beschreven hoe u die toepassing kunt configureren voor bewerkingen die betrekking hebben op privacy. Hieronder ziet u hoe u uw gegevens kunt opmaken en labelen. Er zijn twee categorieën aanvragen:

* [Toepassingen die zijn geïntegreerd met de privacyservice](#integrated): Toepassingen die toegang kunnen verzenden, aanvragen kunnen verwijderen of weigeren naar de privacyservice.
* [Zelfservertoepassingen](#self-serve): Toepassingen die hun privacyverzoeken intern moeten beheren en niet rechtstreeks met de privacyservice kunnen communiceren.

Raadpleeg de documentatie bij uw Experience Cloud-toepassingen voor meer informatie over het opmaken van uw privacyverzoeken en over de waarden die worden ondersteund voor deze aanvragen.

## Toepassingen die zijn geïntegreerd met de privacyservice {#integrated}

Hieronder volgt een lijst met Experience Cloud-toepassingen die zijn geïntegreerd met de Privacy Service, waaronder de mogelijkheden van de Privacy Service waarmee ze compatibel zijn, en koppelingen naar documentatie voor meer informatie.

| Toepassing | Toegang/verwijderen | Uitschakelen van verkoop | Documentatie en overwegingen |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Documentatie openen/verwijderen](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>Advertising Cloud maakt gebruik van bestaande wereldwijde opt-out-mogelijkheden van het Adobe Privacy Center. Zie de handleiding over het [maken van privacyverzoeken](https://docs.adobe.com/content/help/en/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) voor gegevens voor meer informatie.</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Documentatie openen/verwijderen](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/index.html)</li><li>Analytics verwerkt opt-out-aanvragen met behulp van variabelen voor [privacyrapportage](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Documentatie openen/verwijderen](https://marketing.adobe.com/resources/help/en_US/aam/aam-gdpr.html)</li><li>[Documentatie bij uitsluiting](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campagne Standard | ✓ | ✓ | <ul><li>[Documentatie openen/verwijderen](https://docs.campaign.adobe.com/doc/standard/getting_started/en/ACS_GDPR.html)</li><li>[Documentatie bij uitsluiting](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Toegang tot/verwijdering van documentatie voor het Data Lake](../catalog/privacy.md)</li><li>[Documentatie voor realtime-klantprofiel openen/verwijderen](../profile/privacy.md)</li><li>Het Platform van de ervaring neemt [opt-out verzoeken voor publiekssegmenten](../segmentation/honoring-opt-outs.md)in acht.</li></ul> |
| Adobe Primetime-verificatie | ✓ | N.v.t. | <ul><li>[Documentatie openen/verwijderen](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Primetime beschikt niet over de mogelijkheid om gegevens over te dragen, en daarom zijn aanvragen om te weigeren van verkoop niet van toepassing.</li></ul> |
| Adobe-doel | ✓ | N.v.t. | <ul><li>[Documentatie openen/verwijderen](https://marketing.adobe.com/resources/help/en_US/target/target/privacy-and-general-data-protection-regulation.html)</li><li>Het doel beschikt niet over de mogelijkheid om gegevens over te dragen, zodat aanvragen om niet in de handel te worden genomen niet van toepassing zijn.</li></ul> |

<!-- (To include once access/delete documentation is available)
Adobe Customer Attributes (CRS) | ✓ | N/A | <ul><li>Customer Attributes does not have the capability to transfer data, therefore opt-out-of-sale requests are not applicable.</li></ul>
-->

## Zelfservertoepassingen {#self-serve}

Hieronder volgt een lijst met Experience Cloud-toepassingen die niet zijn geïntegreerd met de Privacy Service en die hun privacyproblemen intern moeten beheren. Koppelingen naar de documentatie van elke toepassing worden gegeven, samen met een beschrijving van de inhoud van de documentatie.

| Toepassing | Documentatiebeschrijving |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/ACC_GDPR.html) | Een overzicht van de GDPR-functies voor Adobe Campaign Classic. |
| [Adobe Dynamic Tag Manager](https://marketing.adobe.com/resources/help/en_US/dtm/opt-in.html) | Stappen om te voorkomen dat Adobe-tags worden geactiveerd totdat de toestemming is verkregen. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Een overzicht van hoe een beheerder van de klantenprivacy of beheerder AEM GDPR- verzoeken kan behandelen. |
| [Adobe Experience Manager Live](https://marketing.adobe.com/resources/help/en_US/livefyre/c_gdpr_compliance.html) | Stappen voor het maken van GDPR toegang en schrapping verzoeken gebruikend Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Hoe ontwikkelaars uitbreidingen en de regelbouwer kunnen gebruiken om opt-in en opt-out oplossingen te bepalen. |
| [Adobe Social](https://marketing.adobe.com/resources/help/en_US/social/c_gdpr-request.html) | Stappen voor het gebruik van het GDPR-aanvraagformulier voor toegang tot of verwijdering van door Social verzamelde gegevens. |