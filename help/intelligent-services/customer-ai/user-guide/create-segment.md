---
keywords: Experience Platform;inzichten;klantenai;populaire onderwerpen;klantenai segmenten
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Klantsegmenten maken met voorspelde scores
description: Wanneer een voorspelling is voltooid, worden voorspelde scores voor de dichtheid automatisch verbruikt door Profielen. Door profielen te verrijken met AI-scores van de Klant, kunnen klantsegmenten worden gemaakt om een publiek te zoeken op basis van hun populatiescore. Deze sectie verstrekt stappen voor het creëren van segmenten gebruikend de Bouwer van het Segment.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: 68aa226395e8dcbf98a851134332f31303a8c710
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Maak klantsegmenten met voorspelde scores

Wanneer een voorspelling is voltooid, worden voorspelde scores voor de dichtheid automatisch verbruikt door Profielen. Door profielen te verrijken met AI-scores van de Klant, kunnen klantsegmenten worden gemaakt om een publiek te zoeken op basis van hun populatiescore. Deze sectie verstrekt stappen voor het creëren van segmenten gebruikend de Bouwer van het Segment. Voor een robuustere zelfstudie over het maken van segmenten raadpleegt u de [Gebruikershandleiding voor Segment Builder](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Om deze methode te gebruiken, moet het Profiel van de Klant in real time voor de dataset worden toegelaten.

Klik in de interface van het platform op **[!UICONTROL Segments]** in de linkernavigatie, en klik dan **[!UICONTROL Create segment]**.

![](../images/user-guide/segments_new.png)

De **Segment Builder** wordt weergegeven. Van links **[!UICONTROL Fields]** en onder de **[!UICONTROL Attributes]** tab, klik op de map met de naam **[!UICONTROL XDM Individual Profile]** en klik vervolgens op de map met de naamruimte van uw organisatie. De benoemde map **[!UICONTROL Customer AI]** bevat de resultaten van voorspellingslooppas en genoemd naar de instantie de scores tot behoren. Klik op een instantiemap om de resultaten van de gewenste instantie te openen.

![](../images/user-guide/results_new.png)

In het midden van Segment Builder kunt u de **[!UICONTROL Score]** kenmerk op de *regelbouwcanvas* om een regel te definiëren.

Rechts onder *Segmenteigenschappen* een naam voor het segment opgeven.

![](../images/user-guide/properties_new.png)

Boven de linkerkant *Velden* kolom, klikt u op de **tandwiel** en selecteert u een *Samenvoegbeleid* in de vervolgkeuzelijst. Klikken **[!UICONTROL Save]** om het segment te maken.

![](../images/user-guide/merge_policy_new.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een publiek gevonden dat is gebaseerd op hun populiteitsscores met de Segment Builder. U kunt uw publiek nu richten door hen aan bestemmingen te activeren. Zie de [Overzicht van doelen](../../../destinations/home.md) voor meer informatie .
