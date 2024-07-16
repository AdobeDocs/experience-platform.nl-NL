---
title: API-overzicht van Edge Network
description: Leer wat de Server API van de Edge Network is en hoe u het kunt gebruiken.
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: 041a1782442df5f08bb52e4e450734a51c7781ea
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# API-overzicht van Edge Network {#overview}

De Adobe Experience Platform Edge Network biedt klanten een geoptimaliseerde manier om te communiceren met Adobe Experience Cloud- of Adobe Experience Platform Edge-services.

[!DNL Edge Network Server API] kan worden gebruikt voor verschillende gevallen van gegevensverzameling, personalisatie, reclame en marketing. [!DNL Server API] kan op servers, [!DNL IoT] apparaten, reeks-hoogste dozen, en diverse andere apparaten worden gebruikt.

Aangezien [!DNL Server API] niet afhankelijk is van te laden bibliotheken, biedt het een bliksemsnelle manier om te communiceren met de Adobe Experience Platform-Edge Network en de ondersteunde oplossingen.

De voordelen van de [!DNL Server API] -architectuur zijn onder andere:

* Lagere laadtijd van pagina
* Verbeterde latentie
* Gegevensverzameling van eerste partijen
* Gestroomlijnde, server-zijmededeling tussen de diensten

[!DNL Server API] ondersteunt interactieve gegevensverzameling en batchgegevensverzameling via twee speciale eindpunten:

1. Het interactieve eindpunt steunt communicatie met de diensten van Adobe Experience Platform en van Adobe Experience Cloud die geavanceerde segmentatie, verpersoonlijking, en andere marketing gebruiksgevallen steunen.
2. Het batcheindpunt staat verzoeken toe om in partij worden verzonden wanneer de gegevens moeten worden gecontroleerd zonder een reactie van de toepassingen te ontvangen die worden geroepen.

[!DNL Server API] steunt het volgende type van verzoeken:

* Voor authentiek verklaarde verzoeken via [ Adobe Developer ](https://developer.adobe.com/), gebruikend het `server.adobedc.net` eindpunt.
* Niet-geverifieerde aanvragen via het `edge.adobedc.net` eindpunt.

Dit laat gebruiksgevallen toe die voor veilige, voor authentiek verklaarde inzameling van gevoelige gegevens, volgens het privacybeleid van uw organisatie toestaan. Naast verificatie biedt de server-API ondersteuning voor het markeren van gegevensstromen, zodat alleen geverifieerde communicatie via de API wordt geaccepteerd.

Bekijk de video hieronder voor een gestroomlijnd overzicht van de server-API.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
