---
keywords: reclame; banden;
title: Microsoft Bing-verbinding
description: Met de Microsoft Bing-verbindingsbestemming kunt u gerichte digitale campagnes heroriënteren en publieksgericht voeren in Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 72225ac673ed921b5857a14070660134949e7e3e
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---

# [!DNL Microsoft Bing] verbinding {#bing-destination}

## Overzicht {#overview}

De [!DNL Microsoft Bing] doel helpt u profielgegevens te verzenden naar [!DNL Microsoft Display Advertising].

Profielgegevens verzenden naar [!DNL Microsoft Bing], moet u eerst verbinding maken met het doel.

## Gebruiksscenario’s {#use-cases}

Als markator wil ik het publiek kunnen gebruiken dat is opgebouwd uit [!DNL Microsoft Advertising IDs] om gebruikers aan te spreken via reclame over [!DNL Microsoft Advertising] kanalen.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Microsoft Bing] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|---|
| GEMAAKT | Microsoft-advertentie-id |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

**[!DNL Audience Export]** - u exporteert alle leden van een publiek naar de [!DNL Microsoft Bing] bestemming.

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek naar de [!DNL Microsoft Bing] bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
>Als u uw eerste bestemming wilt maken met [!DNL Microsoft Bing] en hebben de [ID-synchronisatiefunctie](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in het verleden (met Adobe Audience Manager of andere toepassingen), neemt u contact op met Adobe Consulting of Customer Care om ID syncs in te schakelen. Als u al eerder was ingesteld [!DNL Microsoft Bing] Als u integreert in Audience Manager, worden de id-syncs die u hebt ingesteld, overgedragen naar Platform.

Wanneer het vormen van de bestemming, moet u de volgende informatie verstrekken:

* [!UICONTROL Account ID]: dit is jouw [!DNL Bing Ads CID], in gehele notatie.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL Bing Ads Customer ID] (CID). Uw CID is een geheel getal, dat u kunt vinden in de URL wanneer u zich aanmeldt [!DNL Microsoft Advertising].

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="Toewijzing-id"
>abstract="Voer de numerieke publiek-id voor de ring in waaraan u het geselecteerde segment wilt toewijzen. Indien [!UICONTROL Mapping ID] komt niet overeen met een publieks-id in de Bing-bestemming, worden de verwachte publieksgegevens in uw Bing-account niet weergegeven."

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

In de [Publiek schema](../../ui/activate-segment-streaming-destinations.md#scheduling) stap, moet u de publieksnaam handmatig toewijzen in het dialoogvenster [!UICONTROL Mapping ID] veld. Zo zorgt u ervoor dat de metagegevens van het publiek correct worden doorgegeven aan [!DNL Bing].

![UI-afbeelding die het scherm van het publieksprogramma weergeeft met een voorbeeld van hoe u de publieksnaam kunt toewijzen aan de Bing Mapping-id.](../../assets/catalog/advertising/bing/mapping-id.png)

## Geëxporteerde gegevens {#exported-data}

Controleren of gegevens zijn geëxporteerd naar de [!DNL Microsoft Bing] doel, controleer uw [!DNL Microsoft Bing Ads] account. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.
