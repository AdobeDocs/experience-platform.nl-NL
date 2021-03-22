---
keywords: 'reclame; borden; '
title: Microsoft Bing-verbinding
description: Met de de verbindingsbestemming van de Bing van Microsoft, kunt u het opnieuw richten en publiek gerichte digitale campagnes over de Reclame van de Vertoning van Microsoft uitvoeren.
translation-type: tm+mt
source-git-commit: 24e0a274e61fcf6311c647067920686e4f25e840
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 1%

---


# [!DNL Microsoft Bing] verbinding  {#bing-destination}

## Overzicht {#overview}

Met de bestemming [!DNL Microsoft Bing] kunt u profielgegevens naar [!DNL Microsoft Display Advertising] verzenden.

Als u profielgegevens naar [!DNL Microsoft Bing] wilt verzenden, moet u eerst verbinding maken met het doel.

## Gebruiksscenario’s {#use-cases}

Als markator, wil ik segmenten kunnen gebruiken die van [!DNL Microsoft Advertising IDs] worden gebouwd om gebruikers door vertoningsreclame over [!DNL Microsoft Advertising] kanalen te richten.

## Ondersteunde identiteiten {#supported-identities}

[!DNL The Trade Desk] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|---|
| GEMAAKT | Microsoft Advertising ID |

## Type exporteren {#export-type}

**[!DNL Segment Export]** - u exporteert alle leden van een segment (publiek) naar de  [!DNL Microsoft Bing] bestemming.

## Vereisten {#prerequisites}

Als u uw eerste bestemming met [!DNL Microsoft Bing] wilt maken en in het verleden (met Adobe Audience Manager of andere toepassingen) de [ID-synchronisatiefunctionaliteit](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) niet hebt ingeschakeld in de Experience Cloud ID-service, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder [!DNL Microsoft Bing] integraties in Audience Manager had opgezet, de syncs van identiteitskaart u opstelling dragen over aan Platform.

Wanneer het vormen van de bestemming, moet u de volgende informatie verstrekken:

* [!UICONTROL Account ID]: Dit is uw  [!DNL Bing Ads CID]geheel getal.

## Verbinden met doel {#connect-destination}

Selecteer [!DNL Microsoft Bing] in **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteer **[!UICONTROL Configure]**.

![Bestemming Microsoft Bing configureren](../../assets/catalog/advertising/bing/configure.png)

Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL Activate]** knop op de doelkaart zien. Raadpleeg voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]** de sectie [Catalog](../../ui/destinations-workspace.md#catalog) van de documentatie van de doelwerkruimte.

![Microsoft Bing-doel activeren](../../assets/catalog/advertising/bing/activate.png)

## Verificatiestap {#authentication}

In de stap **[!UICONTROL Authentication]** moet u de gegevens van de bestemmingsverbinding invoeren:

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL Bing Ads CID].
* **[!UICONTROL Marketing action]**: Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Zie de pagina [Gegevensbeheer in Adobe Experience Platform](../../../data-governance/policies/overview.md) voor meer informatie over marketingacties. Zie [Overzicht van beleidsregels voor gegevensgebruik](../../../data-governance/policies/overview.md) voor informatie over de afzonderlijke door Adobe gedefinieerde marketingacties.

![Verificatie van Microsoft Bing-bestemming](../../assets/catalog/advertising/bing/authentication.png)

Klik op **[!UICONTROL Create destination]**. Uw doel is nu gemaakt. U kunt [!UICONTROL Save & Exit] klikken als u segmenten later wilt activeren, of u kunt [!UICONTROL Next] klikken om de werkstroom voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie [Segmenten activeren](#activate-segments) voor de rest van de workflow.

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md#select-attributes) voor informatie over de workflow voor segmentactivering.

In [Segmentprogramma](../../ui/activate-destinations.md#segment-schedule) stap, moet u uw segmenten aan hun overeenkomstige identiteitskaart of vriendschappelijke naam in de bestemming manueel in kaart brengen.

Wanneer het in kaart brengen van segmenten, adviseren wij u de [!DNL Platform] segmentnaam of een kortere vorm van het, voor gemak van gebruik te gebruiken. Nochtans, te hoeven segmentidentiteitskaart of de naam in uw bestemming niet om in uw [!DNL Platform] rekening aan te passen. Elke waarde die u in het toewijzingsveld invoegt, wordt weerspiegeld door het doel.

![Id voor segmenttoewijzing](../../assets/common/segment-mapping-id.png)

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Microsoft Bing Ads]-account om te controleren of gegevens naar de [!DNL Microsoft Bing]-bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.