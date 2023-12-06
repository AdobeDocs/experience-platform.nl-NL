---
title: Overzicht van Edge Network Server API
description: Leer wat de Server API van het Netwerk van Edge is en hoe u het kunt gebruiken.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Overzicht van Edge Network Server API {#overview}

Het Adobe Experience Platform Edge Network biedt klanten een geoptimaliseerde manier om te communiceren met Adobe Experience Cloud- of Adobe Experience Platform Edge-services.

De [!DNL Edge Network Server API] kan worden gebruikt voor diverse gevallen van gegevensverzameling, personalisatie, reclame en marketing. De [!DNL Server API] kan op servers worden gebruikt, [!DNL IoT] apparaten, set-top boxes en verschillende andere apparaten.

Aangezien de [!DNL Server API] is niet afhankelijk van bibliotheken die u wilt laden, maar biedt een bliksemsnelle manier om te communiceren met het Adobe Experience Platform Edge-netwerk en de ondersteunde oplossingen.

De voordelen van de [!DNL Server API] architectuur omvat:

* Lagere laadtijd van pagina
* Verbeterde latentie
* Gegevensverzameling van eerste partijen
* Gestroomlijnde, server-zijmededeling tussen de diensten

De [!DNL Server API] ondersteunt interactieve gegevensverzameling en batchgegevensverzameling via twee specifieke eindpunten:

1. Het interactieve eindpunt steunt communicatie met de diensten van Adobe Experience Platform en van Adobe Experience Cloud die geavanceerde segmentatie, verpersoonlijking, en andere marketing gebruiksgevallen steunen.
2. Het batcheindpunt staat verzoeken toe om in partij worden verzonden wanneer de gegevens moeten worden gecontroleerd zonder een reactie van de toepassingen te ontvangen die worden geroepen.

De [!DNL Server API] ondersteunt het volgende type verzoeken:

* Voor authentiek verklaarde verzoeken via [Adobe Developer](https://developer.adobe.com/), met de `server.adobedc.net` eindpunt.
* Niet-geverifieerde aanvragen via de `edge.adobedc.net` eindpunt.

Dit laat gebruiksgevallen toe die voor veilige, voor authentiek verklaarde inzameling van gevoelige gegevens, volgens het privacybeleid van uw organisatie toestaan. Naast verificatie biedt de server-API ondersteuning voor het markeren van gegevensstromen, zodat alleen geverifieerde communicatie via de API wordt geaccepteerd.

Bekijk de video hieronder voor een gestroomlijnd overzicht van de server-API.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
