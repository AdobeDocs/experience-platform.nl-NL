---
title: Uitgebreide activering van Audience Manager
description: Leer hoe u het publiek van de Audience Manager activeert naar sociale en advertentiebestemmingen, via Uitgebreide activering van de Audience Manager.
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Uitgebreide activering van Audience Manager 

Voortgebouwd op Adobe Experience Platform, de Audience Manager Uitgebreide de hulp van de Activering bestaande [ Audience Manager ](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) gebruikers activeert hun publiek aan [ sociale ](../destinations/catalog/social/overview.md) en [ reclame ](../destinations/catalog/advertising/overview.md) bestemmingsplatforms van Real-Time CDP, zoals [ Facebook ](../destinations/catalog/social/facebook.md), [ Google Adds ](../destinations/catalog/advertising/google-ads-destination.md), en meer.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] is alleen beschikbaar voor bestaande [!DNL Audience Manager] -gebruikers.

## Terminologie {#terminology}

De Audience Manager Uitgebreide Activering gebruikt concepten en componenten van Adobe Experience Platform. Om de uitgebreide workflow voor activering en de componenten die u gebruikt beter te begrijpen, moet u een basiskennis van de volgende concepten hebben:

* [ Soorten publiek ](../segmentation/ui/overview.md): Het publiek is reeksen mensen die gelijkaardig gedrag en/of kenmerken delen. Deze verzameling personen kan door Adobe Experience Platform worden gegenereerd met behulp van segmentdefinities of publiekscompositie (publiek dat door het platform wordt gegenereerd) of met behulp van externe bronnen, zoals aangepaste uploads (extern gegenereerd publiek). In Uitgebreide Activering, worden uw segmenten van de Audience Manager (publiek) ingevoerd als [ douane uploadt ](../segmentation/ui/audience-portal.md#import-audience).
* [ de schakelaars van Source ](../sources/home.md): De schakelaars van Source (die ook als bronnen worden bekend) helpen de gebruikers van het Experience Platform gemakkelijk gegevens uit veelvoudige bronnen opnemen, die het structureren, het etiketteren en de verhoging van gegevens toestaan gebruikend de diensten van het Experience Platform. Gegevens kunnen worden ingevoerd uit verschillende bronnen, zoals cloudgebaseerde opslag, software van derden en CRM-systemen.
* [ de schakelaars van de Bestemming ](../destinations/home.md): De bestemmingen beschrijven om het even welk eindpunt, zoals een toepassing van de Adobe, een reclameplatform, de dienst van de wolkenopslag, of de marketing dienst, waar een publiek wordt geactiveerd en geleverd. [!DNL Expanded Activation] steunt de activering van publiek aan [ reclame ](../destinations/catalog/advertising/overview.md) en [ sociale ](../destinations/catalog/social/overview.md) bestemmingsschakelaars.

## Vereisten {#prerequisites}

Voordat u het publiek kunt activeren door Uitgebreide activering, moet u controleren of aan de onderstaande voorwaarden is voldaan.

### Gebruiker- en rolvereisten {#permission-requirements}

Voordat u [!DNL Expanded Activation] kunt gebruiken, moet u een gebruikersaccount maken van de Admin Console en deze toewijzen aan de [!DNL Expanded Activation] -rol. Zie de [ beleid ](administration.md) pagina voor gedetailleerde instructies op hoe te om dit te doen.

### Eisen inzake het publiek {#audience-requirements}

Om publiek door [!DNL Expanded Activation] te activeren, zorg ervoor dat uw publiek van de Audience Manager op **gehakt e-mailadressen** gebaseerd is. Er zijn twee manieren om dit te verzekeren, gebaseerd op uw gebruik van de Audience Manager:

* Als u de [ Audience Manager op mensen-Gebaseerde functionaliteit van Doelen ](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) gebruikt, dan neemt u reeds gehakte e-mailadressen in Audience Manager op. Er is geen extra stap die u in dit geval moet nemen. U kunt overslaan aan [ activerend publiek door Uitgebreide Activering ](activate-audiences.md).
* Als u _niet_ gebruikend de [ Audience Manager op mensen-Gebaseerde functionaliteit van Doelen ](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) bent, moet u een nieuwe gegevensbron in Audience Manager tot stand brengen, en het gebruiken om gehakt e-mailadressen op te slaan. Zie de documentatie bij [ vormend een gegevensbron voor gehakt e-mailwerkschema&#39;s ](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) om te leren hoe te om dit te doen. Nadat u gehakt e-mailadressen in uw gegevensbron van de Audience Manager hebt ingegeten, lees de documentatie op [ activerend publiek door Uitgebreide Activering ](activate-audiences.md).

## Volgende stappen {#next-steps}

Nu u een beter inzicht in de gebruiksgevallen en de voordelen van het gebruiken [!DNL Expanded Activation] hebt, begin [ vormend uw rekening ](administration.md) en dan [ activeer uw publiek ](activate-audiences.md).
