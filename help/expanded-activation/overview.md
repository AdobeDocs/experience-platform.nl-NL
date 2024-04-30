---
title: Uitgebreide Audience Manager activering
description: Leer hoe u het publiek van de Audience Manager activeert naar sociale en advertentiebestemmingen, via Uitgebreide activering van de Audience Manager.
source-git-commit: 5bc8d6c7173f221c2830a9b15c8ec6241e8bc59d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# Uitgebreide Audience Manager activering

Uitgebreide Audience Manager is gebaseerd op Adobe Experience Platform en helpt bestaande [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) gebruikers activeren hun publiek naar [sociaal](../destinations/catalog/social/overview.md) en [reclame](../destinations/catalog/advertising/overview.md) doelplatforms uit Real-Time CDP, zoals [Facebook](../destinations/catalog/social/facebook.md), [Google Adds](../destinations/catalog/advertising/google-ads-destination.md)en meer.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] is alleen beschikbaar voor bestaande [!DNL Audience Manager] gebruikers.

## Terminologie {#terminology}

De Audience Manager Uitgebreide Activering gebruikt concepten en componenten van Adobe Experience Platform. Om de uitgebreide workflow voor activering en de componenten die u gebruikt beter te begrijpen, moet u een basiskennis van de volgende concepten hebben:

* [Soorten publiek](../segmentation/ui/overview.md): Soorten publiek zijn groepen mensen met een vergelijkbaar gedrag en/of vergelijkbare kenmerken. Deze verzameling personen kan door Adobe Experience Platform worden gegenereerd met behulp van segmentdefinities of publiekscompositie (publiek dat door het platform wordt gegenereerd) of met behulp van externe bronnen, zoals aangepaste uploads (extern gegenereerd publiek). Bij Uitgebreide activering worden de segmenten van uw Audience Manager (soorten publiek) geïmporteerd als [aangepaste uploads](../segmentation/ui/overview.md#import-audience).
* [Bronaansluitingen](../sources/home.md): Bronconnectors (ook wel bronnen genoemd) helpen gebruikers in de Experience Platform gemakkelijk gegevens uit meerdere bronnen in te voeren, zodat ze gegevens kunnen structureren, labelen en verbeteren met behulp van de diensten van het Experience Platform. Gegevens kunnen worden ingevoerd uit verschillende bronnen, zoals cloudgebaseerde opslag, software van derden en CRM-systemen.
* [Aansluitingen bestemming](../destinations/home.md): De bestemmingen beschrijven om het even welk eindpunt, zoals een toepassing van de Adobe, een reclameplatform, de dienst van de cloudopslag, of de marketing dienst, waar een publiek wordt geactiveerd en geleverd. [!DNL Expanded Activation] ondersteunt de activering van het publiek naar [reclame](../destinations/catalog/advertising/overview.md) en [sociaal](../destinations/catalog/social/overview.md) doelconnectors.

## Vereisten {#prerequisites}

Voordat u het publiek kunt activeren door Uitgebreide activering, moet u controleren of aan de onderstaande voorwaarden is voldaan.

### Gebruiker- en rolvereisten {#permission-requirements}

Wat u moet doen [!DNL Expanded Activation], moet u een gebruikersaccount maken van de Admin Console en deze toewijzen aan de [!DNL Expanded Activation] rol. Zie de [administratie](administration.md) pagina voor gedetailleerde instructies over hoe te om dit te doen.

### Eisen inzake het publiek {#audience-requirements}

Het publiek activeren via [!DNL Expanded Activation], zorg ervoor dat uw publiek van de Audience Manager op **gehashte e-mailadressen**. Er zijn twee manieren om dit te verzekeren, gebaseerd op uw gebruik van de Audience Manager:

* Als u het [Audience Manager op mensen gebaseerde bestemmingen](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) -functionaliteit hebt, neemt u al gehashte e-mailadressen in Audience Manager in. Er is geen extra stap die u in dit geval moet nemen. U kunt overslaan naar [activeren van het publiek via Uitgebreide activering](activate-audiences.md).
* Als u _niet_ met de [Audience Manager op mensen gebaseerde bestemmingen](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) , moet u een nieuwe gegevensbron in de Audience Manager maken en deze gebruiken om gehashte e-mailadressen op te slaan. Zie de documentatie op [configureren van een gegevensbron voor gehashte e-mailworkflows](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) om te leren hoe u dit kunt doen. Nadat u gehashte e-mailadressen in uw gegevensbron van de Audience Manager hebt opgenomen, lees de documentatie op [activeren van het publiek via Uitgebreide activering](activate-audiences.md).

## Volgende stappen {#next-steps}

Nu u een beter inzicht hebt in de gebruiksgevallen en -voordelen van het gebruik [!DNL Expanded Activation], start [configureren, account](administration.md) en vervolgens [uw publiek activeren](activate-audiences.md).

