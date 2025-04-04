---
solution: Experience Platform
title: Update voor jaartijdbeperking negeren
description: Leer hoe u een probleem kunt oplossen met de tijdsbeperking voor het negeren van het jaar.
hidefromtoc: true
exl-id: 44bb8817-e32d-4806-ad4e-b1840313e768
source-git-commit: c7d71113ddcef6aca8b2637814b46e589a6b7fdf
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Update voor jaartijdbeperking negeren {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="Jaarupdate negeren"
>abstract="De tijdsbeperking voor het negeren van het jaar is bijgewerkt. Sla uw publiek opnieuw op."

>[!IMPORTANT]
>
>U kunt de &quot;negeren jaar&quot;tijdbeperking in een gesegmenteerde segmentdefinitie slechts gebruiken gebruikend **partijsegmentatie**. Toevoegend de &quot;negeren jaar&quot;tijdbeperking aan uw segmentdefinitie zal het resulterende publiek **niet in aanmerking komende** voor het stromen of randsegmentatie maken.

In de release van februari 2024 voor Adobe Experience Platform zijn wijzigingen aangebracht in de Adobe Experience Platform Segmentation Service, die een probleem verhelpt met de optie &#39;jaar negeren&#39; bij het creëren en evalueren van het publiek.

De optie &#39;Jaar negeren&#39; is bedoeld om de jaarcomponent van een datum te negeren bij het uitvoeren van publieksevaluaties. U kunt deze optie gebruiken in situaties waarin de tijdsrelatie tussen verschillende gebeurtenissen belangrijk is, maar het specifieke jaar niet belangrijk is, zoals een veld voor de geboortedatum.

In schrikkeljaren zoals 2024 kon het onderliggende systeem deze optie echter niet goed verwerken, wat leidde tot onjuiste publieksevaluaties. Als het &quot;jaar negeren&quot; in een schrikkeljaar wordt ingeschakeld, zal de publieksevaluatie een dag voorbij gaan.

Als u een publiek creeerde alvorens deze moeilijke situatie werd vrijgegeven, moet u enkel het publiek in de Bouwer van het Segment opnieuw opslaan om de moeilijke situatie toe te passen. Als u niet zeker bent of wordt uw publiek beïnvloed door deze resolutie, zal de Bouwer van het Segment de gebruiker op de hoogte brengen als het bestaande publiek door deze kwestie wordt beïnvloed.
