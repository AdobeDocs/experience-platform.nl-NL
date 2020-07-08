---
keywords: Experience Platform;insights; customer ai;popular topics
solution: Experience Platform
title: Maak klantsegmenten met voorspelde scores
topic: Create a segment
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---


# Maak klantsegmenten met voorspelde scores

Wanneer een voorspelling is voltooid, worden voorspelde scores voor de dichtheid automatisch verbruikt door profielen. Door profielen te verrijken met AI-scores van de Klant, kunnen klantsegmenten worden gemaakt om een publiek te zoeken op basis van hun populatiescore. Deze sectie verstrekt stappen voor het creëren van segmenten gebruikend de Bouwer van het Segment. Voor een robuustere zelfstudie over het maken van segmenten raadpleegt u de gebruikershandleiding [van](../../../segmentation/tutorials/create-a-segment.md)Segment Builder.

>[!IMPORTANT]
>
>Om deze methode te gebruiken, moet het Profiel van de Klant in real time voor de dataset worden toegelaten.

In het Platform UI, klik **[!UICONTROL Segmenten]** in de linkernavigatie, en klik dan **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

De *Segment Builder* wordt weergegeven. Klik in de linkerkolom *Velden* en onder het tabblad *Kenmerken* op de map **[!UICONTROL XDM Individueel profiel]** en klik vervolgens op de map met de naamruimte van uw organisatie. De map met de naam **[!UICONTROL Customer AI]** bevat de resultaten van voorspellingen en krijgt de naam van de instantie waartoe de scores behoren. Klik op een instantiemap om de resultaten van de gewenste instantie te openen.

![](../images/user-guide/results.png)

Bevestigd in het centrum van de Bouwer van het Segment, sleep en laat vallen de attributen van de **[!UICONTROL Score]** op het canvas *van de* regelbouwer om een regel te bepalen.

Geef een naam voor het segment op onder de eigenschappenkolom *Segment aan de rechterkant* .

![](../images/user-guide/properties.png)

Klik boven de linkerkolom *Velden* op het **tandwielpictogram** en selecteer een beleid *voor* samenvoegen in de vervolgkeuzelijst. Klik op **[!UICONTROL Opslaan]** om het segment te maken.

![](../images/user-guide/merge_policy.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een publiek gevonden dat is gebaseerd op hun populiteitsscores met de Segment Builder. U kunt uw publiek nu richten door hen aan bestemmingen te activeren. Zie het [bestemmingsoverzicht](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) voor meer informatie.