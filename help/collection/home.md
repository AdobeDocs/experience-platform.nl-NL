---
solution: Experience Platform
title: Overzicht van gegevensverzameling
description: Leer hoe u gegevens naar Adobe Experience Platform verzendt.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 3d51f01d314587510d900d335dc92fedb8ac31e8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# Overzicht van gegevensverzameling

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens van klanten kunt verzamelen en naar Adobe Experience Platform Edge Network kunt verzenden. Die gegevens kunnen vervolgens worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

Adobe ondersteunt de volgende codetalen met speciale bibliotheken voor gegevensverzameling:

* **JavaScript**: Voor websites en web-based toepassingen
* **Kotlin**: Voor de apparaten van Android
* **Swift**: Voor de apparaten van iOS
* **Helderscript**: Voor apparaten van Roku
* **Flutter**: Voor Android + iOS toepassingen die Flutter gebruiken
* **React Native**: Voor Android + iOS toepassingen die React Native gebruiken

De tags UI in de gegevensverzameling van Adobe Experience Platform omvat de extensie Web SDK en Mobile SDK.

Als geen van bovengenoemde SDKs de behoeften van uw project aanpast, kunt u [ Adobe Experience Platform Edge Network API ](https://developer.adobe.com/data-collection-apis/docs/) gebruiken om gegevens rechtstreeks naar Adobe te verzenden.

## Gegevensverzamelingsproces

In plaats van afzonderlijke bibliotheken voor elk Adobe-product te installeren en te implementeren, kunt u een van de bovenstaande SDK&#39;s of tagextensies implementeren om alle gewenste gegevens samen te voegen tot één enkele lading. Die nuttige lading wordt verzonden naar a [ datastream ](/help/datastreams/overview.md) in Adobe Experience Platform Edge Network.

![ het diagram van de inzameling van Gegevens ](assets/tags-sdks.png)

De Adobe Experience Platform Edge Network is een wereldwijd gedistribueerd, snel en betrouwbaar netwerk van servers die gegevens op enorme schaal kunnen ontvangen en verwerken. Wanneer een gegevensstroom gegevens ontvangt, verspreidt het die gegevens aan elke respectieve oplossing die u hebt gevormd. De gegevens worden doorgegeven in een indeling die elk afzonderlijk product begrijpt.

![ Adobe oplossingsdiagram ](assets/adobe-solutions.png)

U kunt [ gebeurtenis ook gebruiken door:sturen ](/help/tags/ui/event-forwarding/overview.md) om, gegevens aan om het even welke niet bestemming van Adobe met lage latentie en zonder om het even welke cliënt-kant implementatiecode te transformeren te verrijken en te verzenden.

![ Gebeurtenis door:sturen diagram ](assets/event-forwarding.png)
