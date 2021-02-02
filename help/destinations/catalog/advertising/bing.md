---
keywords: 'reclame; borden; '
title: Microsoft Bing-doel
seo-title: Met de Microsoft Bing-bestemming kunt u profielgegevens naar Microsoft Display Advertising verzenden.
description: Met de bestemming van de Bing van Microsoft, kunt u het opnieuw richten en publiek gerichte digitale campagnes over de Reclame van de Vertoning van Microsoft uitvoeren.
seo-description: Met de bestemming van de Bing van Microsoft, kunt u het opnieuw richten en publiek gerichte digitale campagnes over de Reclame van de Vertoning van Microsoft uitvoeren.
translation-type: tm+mt
source-git-commit: 95f57f9d1b3eeb0b16ba209b9774bd94f5758009
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---


# [!DNL Microsoft Bing] doel

## Overzicht {#overview}

Met de bestemming [!DNL Microsoft Bing] kunt u profielgegevens naar [!DNL Microsoft Display Advertising] verzenden.

Als u profielgegevens naar [!DNL Microsoft Bing] wilt verzenden, moet u eerst verbinding maken met het doel.

## Doelspecificaties {#destination-specs}

Let op de volgende details die specifiek zijn voor het doel [!DNL Microsoft Bing]:

* U kunt de volgende [identiteiten](../../../identity-service/namespaces.md) naar [!DNL Microsoft Bing] bestemmingen verzenden: [!DNL Microsoft ID].

## Gebruiksscenario’s {#use-cases}

Als markator, wil ik segmenten kunnen gebruiken die van [!DNL Microsoft Advertising IDs] worden gebouwd om gebruikers door vertoningsreclame over [!DNL Microsoft Advertising] kanalen te richten.

## Type exporteren {#export-type}

**[!DNL Segment Export]** - u exporteert alle leden van een segment (publiek) naar de  [!DNL Microsoft Bing] bestemming.

## Vereisten {#prerequisites}

Wanneer het vormen van de bestemming zult u worden gevraagd om de volgende informatie te verstrekken:

* [!UICONTROL Account-id]: Dit is uw  [!DNL Bing Ads CID]geheel getal.

## Verbinden met doel {#connect-destination}

Selecteer **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]** en selecteer [!DNL Microsoft Bing] en **[!UICONTROL Configureren]**.

![Bestemming Microsoft Bing configureren](../../assets/catalog/advertising/bing/configure.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL knop Activeer]** op de doelkaart zien. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar [Catalog](../../ui/destinations-workspace.md#catalog) sectie van de documentatie van de bestemmingswerkruimte.
>
>![Microsoft Bing-doel activeren](../../assets/catalog/advertising/bing/activate.png)

In [!UICONTROL Authentificatie] stap, moet u de details van de bestemmingsverbinding ingaan:

* **[!UICONTROL Naam]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Omschrijving]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account-id]**: Je  [!DNL Bing Ads CID].
* **[!UICONTROL Geval]** voor gebruik bij het in de handel brengen: Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Zie de pagina [Gegevensbeheer in Adobe Experience Platform](../../../data-governance/policies/overview.md) voor meer informatie over gevallen van marketinggebruik. Zie [Overzicht van beleidsregels voor gegevensgebruik](../../../data-governance/policies/overview.md) voor informatie over de afzonderlijke door Adobe gedefinieerde gevallen van marketinggebruik.

![Verificatie van Microsoft Bing-bestemming](../../assets/catalog/advertising/bing/authentication.png)

Klik **[!UICONTROL Doel maken]**. Uw doel is nu gemaakt. U kunt [!UICONTROL Opslaan &amp; afsluiten] klikken als u segmenten later wilt activeren, of u kunt [!UICONTROL Volgende] klikken om de workflow voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie [Segmenten activeren](#activate-segments) voor de rest van de workflow.

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md#select-attributes) voor informatie over de workflow voor segmentactivering.

In [Segmentprogramma](../../ui/activate-destinations.md#segment-schedule) stap, moet u uw segmenten aan hun overeenkomstige identiteitskaart of vriendschappelijke naam in de bestemming manueel in kaart brengen.

Wanneer het in kaart brengen van segmenten, adviseren wij u de [!DNL Platform] segmentnaam of een kortere vorm van het, voor gemak van gebruik te gebruiken. Nochtans, te hoeven segmentidentiteitskaart of de naam in uw bestemming niet om in uw [!DNL Platform] rekening aan te passen. Elke waarde die u in het toewijzingsveld invoegt, wordt weerspiegeld door het doel.

![Id voor segmenttoewijzing](../../assets/common/segment-mapping-id.png)

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Microsoft Bing Ads]-account om te controleren of gegevens naar de [!DNL Microsoft Bing]-bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.