---
keywords: Experience Platform;inzichten;klantenai;populaire onderwerpen;klantenai segmenten
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Klantsegmenten maken met voorspelde scores
topic-legacy: Create a segment
description: Wanneer een voorspelling is voltooid, worden voorspelde scores voor de dichtheid automatisch verbruikt door profielen. Door profielen te verrijken met AI-scores van de Klant, kunnen klantsegmenten worden gemaakt om een publiek te zoeken op basis van hun populatiescore. Deze sectie verstrekt stappen voor het creëren van segmenten gebruikend de Bouwer van het Segment.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Maak klantsegmenten met voorspelde scores

Wanneer een voorspelling is voltooid, worden voorspelde scores voor de dichtheid automatisch verbruikt door profielen. Door profielen te verrijken met AI-scores van de Klant, kunnen klantsegmenten worden gemaakt om een publiek te zoeken op basis van hun populatiescore. Deze sectie verstrekt stappen voor het creëren van segmenten gebruikend de Bouwer van het Segment. Voor een robuustere zelfstudie over het maken van segmenten raadpleegt u de [gebruikershandleiding voor segmentbouwer](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Om deze methode te gebruiken, moet het Profiel van de Klant in real time voor de dataset worden toegelaten.

In Platform UI, klik **[!UICONTROL Segments]** in de linkernavigatie, en klik dan **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

De **Segment Builder** verschijnt. Klik in de linkerkolom **[!UICONTROL Fields]** en onder het tabblad **[!UICONTROL Attributes]** op de map met de naam **[!UICONTROL XDM Individual Profile]** en klik vervolgens op de map met de naamruimte van uw organisatie. De map met de naam **[!UICONTROL Customer AI]** bevat de resultaten van voorspelling en krijgt een naam na de instantie waartoe de scores behoren. Klik op een instantiemap om de resultaten van de gewenste instantie te openen.

![](../images/user-guide/results.png)

In het centrum van de Bouwer van het Segment, belemmering en laat vallen **[!UICONTROL Score]** attribuut op *regelbouwer canvas* om een regel te bepalen.

Geef onder de rechterkolom *Segmenteigenschappen* een naam voor het segment op.

![](../images/user-guide/properties.png)

Klik boven de linkerkolom *Fields* op het pictogram **versnelling** en selecteer een *Samenvoegen-beleid* in de vervolgkeuzelijst. Klik **[!UICONTROL Save]** om het segment tot stand te brengen.

![](../images/user-guide/merge_policy.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een publiek gevonden dat is gebaseerd op hun populiteitsscores met de Segment Builder. U kunt uw publiek nu richten door hen aan bestemmingen te activeren. Zie [bestemmingen overzicht](../../../destinations/home.md) voor meer informatie.
