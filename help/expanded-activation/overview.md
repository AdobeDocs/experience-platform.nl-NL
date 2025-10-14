---
title: 'Uitgebreide activering van Audience Manager '
description: Leer hoe u het Audience Manager-publiek activeert naar sociale en advertentiebestemmingen via Audience Manager Expanded Activation.
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# Uitgebreide activering van Audience Manager 

Voortgebouwd op Adobe Experience Platform, de Audience Manager Uitgebreide hulp van de Activering bestaande [&#x200B; Audience Manager &#x200B;](https://experienceleague.adobe.com/nl/docs/audience-manager/user-guide/aam-home) gebruikers activeert hun publiek aan [&#x200B; sociale &#x200B;](../destinations/catalog/social/overview.md) en [&#x200B; reclame &#x200B;](../destinations/catalog/advertising/overview.md) bestemmingsplatforms van Real-Time CDP, zoals [&#x200B; Facebook &#x200B;](../destinations/catalog/social/facebook.md), [&#x200B; Advertentie van Google &#x200B;](../destinations/catalog/advertising/google-ads-destination.md), en meer.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] is alleen beschikbaar voor bestaande [!DNL Audience Manager] -gebruikers.

## Terminologie {#terminology}

Audience Manager Expanded Activation gebruikt concepten en componenten uit Adobe Experience Platform. Om de uitgebreide workflow voor activering en de componenten die u gebruikt beter te begrijpen, moet u een basiskennis van de volgende concepten hebben:

* [&#x200B; Soorten publiek &#x200B;](../segmentation/ui/overview.md): Het publiek is reeksen mensen die gelijkaardig gedrag en/of kenmerken delen. Deze verzameling personen kan worden gegenereerd door Adobe Experience Platform met behulp van segmentdefinities of publiekscompositie (door Experience Platform gegenereerd publiek) of door externe bronnen, zoals aangepaste uploads (extern gegenereerd publiek). In Uitgebreide Activering, worden uw segmenten van Audience Manager (publiek) ingevoerd als [&#x200B; douane uploadt &#x200B;](../segmentation/ui/audience-portal.md#import-audience).
* [&#x200B; de schakelaars van Source &#x200B;](../sources/home.md): De schakelaars van Source (die ook als bronnen worden bekend) helpen de gebruikers van Experience Platform gegevens uit veelvoudige bronnen gemakkelijk invoeren, die het structureren, het etiketteren en de verhoging van gegevens toestaan gebruikend de diensten van Experience Platform. Gegevens kunnen worden ingevoerd uit verschillende bronnen, zoals cloudgebaseerde opslag, software van derden en CRM-systemen.
* [&#x200B; de schakelaars van de Bestemming &#x200B;](../destinations/home.md): De bestemmingen beschrijven om het even welk eindpunt, zoals een toepassing van Adobe, een reclameplatform, de dienst van de wolkenopslag, of de marketing dienst, waar een publiek wordt geactiveerd en geleverd. [!DNL Expanded Activation] steunt de activering van publiek aan [&#x200B; reclame &#x200B;](../destinations/catalog/advertising/overview.md) en [&#x200B; sociale &#x200B;](../destinations/catalog/social/overview.md) bestemmingsschakelaars.

## Vereisten {#prerequisites}

Voordat u het publiek kunt activeren door Uitgebreide activering, moet u controleren of aan de onderstaande voorwaarden is voldaan.

### Gebruiker- en rolvereisten {#permission-requirements}

Voordat u [!DNL Expanded Activation] kunt gebruiken, moet u een gebruikersaccount maken via de Admin Console en deze toewijzen aan de [!DNL Expanded Activation] -rol. Zie de [&#x200B; beleid &#x200B;](administration.md) pagina voor gedetailleerde instructies op hoe te om dit te doen.

### Eisen inzake het publiek {#audience-requirements}

Om publiek door [!DNL Expanded Activation] te activeren, zorg ervoor dat uw publiek van Audience Manager op **gehakt e-mailadressen** gebaseerd is. Op basis van uw Audience Manager-gebruik zijn er twee manieren om dit te garanderen:

* Als u [&#x200B; Audience Manager op mensen-Gebaseerde Doelen &#x200B;](https://experienceleague.adobe.com/nl/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) functionaliteit gebruikt, dan neemt u reeds gehakte e-mailadressen in Audience Manager op. Er is geen extra stap die u in dit geval moet nemen. U kunt overslaan aan [&#x200B; activerend publiek door Uitgebreide Activering &#x200B;](activate-audiences.md).
* Als u _niet_ gebruikend de [&#x200B; Audience Manager op mensen-Gebaseerde functionaliteit van Doelen &#x200B;](https://experienceleague.adobe.com/nl/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) bent, moet u een nieuwe gegevensbron in Audience Manager tot stand brengen, en het gebruiken om gehakt e-mailadressen op te slaan. Zie de documentatie bij [&#x200B; vormend een gegevensbron voor gehakt e-mailwerkschema&#39;s &#x200B;](https://experienceleague.adobe.com/nl/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) om te leren hoe te om dit te doen. Nadat u gehakt e-mailadressen in uw gegevensbron van Audience Manager hebt ingegeten, lees de documentatie op [&#x200B; activerend publiek door Uitgebreide Activering &#x200B;](activate-audiences.md).

## Volgende stappen {#next-steps}

Nu u een beter inzicht in de gebruiksgevallen en de voordelen van het gebruiken [!DNL Expanded Activation] hebt, begin [&#x200B; vormend uw rekening &#x200B;](administration.md) en dan [&#x200B; activeer uw publiek &#x200B;](activate-audiences.md).
