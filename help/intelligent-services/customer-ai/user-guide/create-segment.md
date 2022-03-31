---
keywords: Experience Platform;inzichten;klanten ai;populaire onderwerpen;klant ai segmenten
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Klantsegmenten maken met voorspelde scores
topic-legacy: Create a segment
description: Wanneer een voorspelling is voltooid, worden voorspelde scores voor de dichtheid automatisch verbruikt door Profielen. Door profielen te verrijken met AI-scores van de Klant, kunnen klantsegmenten worden gemaakt om een publiek te zoeken op basis van hun populatiescore. Deze sectie verstrekt stappen voor het creëren van segmenten gebruikend de Bouwer van het Segment.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Maak klantsegmenten met voorspelde scores

Wanneer een voorspelling is voltooid, worden voorspelde scores voor de dichtheid automatisch verbruikt door Profielen. Door profielen te verrijken met AI-scores van de Klant, kunnen klantsegmenten worden gemaakt om een publiek te zoeken op basis van hun populatiescore. Deze sectie verstrekt stappen voor het creëren van segmenten gebruikend de Bouwer van het Segment. Voor een robuustere zelfstudie over het maken van segmenten raadpleegt u de [Gebruikershandleiding voor Segment Builder](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Om deze methode te gebruiken, moet het Profiel van de Klant in real time voor de dataset worden toegelaten.

Klik in de gebruikersinterface van het Platform op **[!UICONTROL Segments]** in de linkernavigatie, en klik dan **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

De **Segment Builder** wordt weergegeven. Van links **[!UICONTROL Fields]** en onder de **[!UICONTROL Attributes]** tab, klik op de map met de naam **[!UICONTROL XDM Individual Profile]** en klik vervolgens op de map met de naamruimte van uw organisatie. De benoemde map **[!UICONTROL Customer AI]** bevat de resultaten van voorspellingslooppas en genoemd naar de instantie de scores tot behoren. Klik op een instantiemap om de resultaten van de gewenste instantie te openen.

![](../images/user-guide/results.png)

In het midden van Segment Builder kunt u de **[!UICONTROL Score]** kenmerk op de *regelbouwcanvas* om een regel te definiëren.

Onder de rechterhand *Segmenteigenschappen* een naam voor het segment opgeven.

![](../images/user-guide/properties.png)

Boven de linkerkant *Velden* kolom, klikt u op de knop **tandwiel** en selecteert u een *Samenvoegbeleid* in de vervolgkeuzelijst. Klikken **[!UICONTROL Save]** om het segment te maken.

![](../images/user-guide/merge_policy.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een publiek gevonden dat is gebaseerd op hun populiteitsscores met de Segment Builder. U kunt uw publiek nu richten door hen aan bestemmingen te activeren. Zie de [Overzicht van doelen](../../../destinations/home.md) voor meer informatie .
