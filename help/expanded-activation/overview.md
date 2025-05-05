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

Voortgebouwd op Adobe Experience Platform, de Audience Manager Uitgebreide hulp van de Activering bestaande [ Audience Manager ](https://experienceleague.adobe.com/nl/docs/audience-manager/user-guide/aam-home) gebruikers activeert hun publiek aan [ sociale ](../destinations/catalog/social/overview.md) en [ reclame ](../destinations/catalog/advertising/overview.md) bestemmingsplatforms van Real-Time CDP, zoals [ Facebook ](../destinations/catalog/social/facebook.md), [ Advertentie van Google ](../destinations/catalog/advertising/google-ads-destination.md), en meer.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] is alleen beschikbaar voor bestaande [!DNL Audience Manager] -gebruikers.

## Terminologie {#terminology}

Audience Manager Expanded Activation gebruikt concepten en componenten uit Adobe Experience Platform. Om de uitgebreide workflow voor activering en de componenten die u gebruikt beter te begrijpen, moet u een basiskennis van de volgende concepten hebben:

* [ Soorten publiek ](../segmentation/ui/overview.md): Het publiek is reeksen mensen die gelijkaardig gedrag en/of kenmerken delen. Deze verzameling personen kan worden gegenereerd door Adobe Experience Platform met behulp van segmentdefinities of publiekscompositie (door Experience Platform gegenereerd publiek) of door externe bronnen, zoals aangepaste uploads (extern gegenereerd publiek). In Uitgebreide Activering, worden uw segmenten van Audience Manager (publiek) ingevoerd als [ douane uploadt ](../segmentation/ui/audience-portal.md#import-audience).
* [ de schakelaars van Source ](../sources/home.md): De schakelaars van Source (die ook als bronnen worden bekend) helpen de gebruikers van Experience Platform gegevens uit veelvoudige bronnen gemakkelijk invoeren, die het structureren, het etiketteren en de verhoging van gegevens toestaan gebruikend de diensten van Experience Platform. Gegevens kunnen worden ingevoerd uit verschillende bronnen, zoals cloudgebaseerde opslag, software van derden en CRM-systemen.
* [ de schakelaars van de Bestemming ](../destinations/home.md): De bestemmingen beschrijven om het even welk eindpunt, zoals een toepassing van Adobe, een reclameplatform, de dienst van de wolkenopslag, of de marketing dienst, waar een publiek wordt geactiveerd en geleverd. [!DNL Expanded Activation] steunt de activering van publiek aan [ reclame ](../destinations/catalog/advertising/overview.md) en [ sociale ](../destinations/catalog/social/overview.md) bestemmingsschakelaars.

## Vereisten {#prerequisites}

Voordat u het publiek kunt activeren door Uitgebreide activering, moet u controleren of aan de onderstaande voorwaarden is voldaan.

### Gebruiker- en rolvereisten {#permission-requirements}

Voordat u [!DNL Expanded Activation] kunt gebruiken, moet u een gebruikersaccount maken via de Admin Console en deze toewijzen aan de [!DNL Expanded Activation] -rol. Zie de [ beleid ](administration.md) pagina voor gedetailleerde instructies op hoe te om dit te doen.

### Eisen inzake het publiek {#audience-requirements}

Om publiek door [!DNL Expanded Activation] te activeren, zorg ervoor dat uw publiek van Audience Manager op **gehakt e-mailadressen** gebaseerd is. Op basis van uw Audience Manager-gebruik zijn er twee manieren om dit te garanderen:

* Als u [ Audience Manager op mensen-Gebaseerde Doelen ](https://experienceleague.adobe.com/nl/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) functionaliteit gebruikt, dan neemt u reeds gehakte e-mailadressen in Audience Manager op. Er is geen extra stap die u in dit geval moet nemen. U kunt overslaan aan [ activerend publiek door Uitgebreide Activering ](activate-audiences.md).
* Als u _niet_ gebruikend de [ Audience Manager op mensen-Gebaseerde functionaliteit van Doelen ](https://experienceleague.adobe.com/nl/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) bent, moet u een nieuwe gegevensbron in Audience Manager tot stand brengen, en het gebruiken om gehakt e-mailadressen op te slaan. Zie de documentatie bij [ vormend een gegevensbron voor gehakt e-mailwerkschema&#39;s ](https://experienceleague.adobe.com/nl/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) om te leren hoe te om dit te doen. Nadat u gehakt e-mailadressen in uw gegevensbron van Audience Manager hebt ingegeten, lees de documentatie op [ activerend publiek door Uitgebreide Activering ](activate-audiences.md).

## Volgende stappen {#next-steps}

Nu u een beter inzicht in de gebruiksgevallen en de voordelen van het gebruiken [!DNL Expanded Activation] hebt, begin [ vormend uw rekening ](administration.md) en dan [ activeer uw publiek ](activate-audiences.md).
