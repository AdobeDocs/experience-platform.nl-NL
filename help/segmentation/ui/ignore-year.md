---
solution: Experience Platform
title: Update voor jaartijdbeperking negeren
description: Leer hoe u een probleem kunt oplossen met de tijdsbeperking voor het negeren van het jaar.
source-git-commit: d0bd7990f0d77cd5f8d30da735b89c188e13c780
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Update voor jaartijdbeperking negeren {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="Jaarupdate negeren"
>abstract="De tijdsbeperking voor het negeren van het jaar is bijgewerkt. Sla uw publiek opnieuw op."

In de release van februari 2024 voor Adobe Experience Platform zijn wijzigingen aangebracht in de Adobe Experience Platform Segmentation Service, die een probleem verhelpt met de optie &#39;jaar negeren&#39; bij het creëren en evalueren van het publiek.

De optie &#39;Jaar negeren&#39; is bedoeld om de jaarcomponent van een datum te negeren bij het uitvoeren van publieksevaluaties. U kunt deze optie gebruiken in situaties waarin de tijdsrelatie tussen verschillende gebeurtenissen belangrijk is, maar het specifieke jaar niet belangrijk is, zoals een veld voor de geboortedatum.

In schrikkeljaren zoals 2024 kon het onderliggende systeem deze optie echter niet goed verwerken, wat leidde tot onjuiste publieksevaluaties. Als het &quot;jaar negeren&quot; in een schrikkeljaar wordt ingeschakeld, zal de publieksevaluatie een dag voorbij gaan.

Als u een publiek creeerde alvorens deze moeilijke situatie werd vrijgegeven, moet u enkel het publiek in de Bouwer van het Segment opnieuw opslaan om de moeilijke situatie toe te passen. Als u niet zeker bent of wordt uw publiek beïnvloed door deze resolutie, zal de Bouwer van het Segment de gebruiker op de hoogte brengen als het bestaande publiek door deze kwestie wordt beïnvloed.
