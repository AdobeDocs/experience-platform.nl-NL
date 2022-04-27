---
keywords: 'reclame; borden; '
title: Microsoft Bing-verbinding
description: Met de Microsoft Bing-verbindingsbestemming kunt u gerichte digitale campagnes heroriënteren en publieksgericht voeren in Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# [!DNL Microsoft Bing] verbinding {#bing-destination}

## Overzicht {#overview}

De [!DNL Microsoft Bing] doel helpt u profielgegevens te verzenden naar [!DNL Microsoft Display Advertising].

Profielgegevens verzenden naar [!DNL Microsoft Bing], moet u eerst verbinding maken met het doel.

## Gebruiksscenario’s {#use-cases}

Als telleraar, wil ik segmenten kunnen gebruiken die van worden gebouwd [!DNL Microsoft Advertising IDs] om gebruikers aan te spreken via reclame over [!DNL Microsoft Advertising] kanalen.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Microsoft Bing] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|---|
| GEMAAKT | Microsoft-advertentie-id |

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

**[!DNL Segment Export]** - u exporteert alle leden van een segment (publiek) naar de [!DNL Microsoft Bing] bestemming.

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) naar de [!DNL Microsoft Bing] bestemming. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
>Als u uw eerste bestemming wilt maken met [!DNL Microsoft Bing] en hebben de [ID-synchronisatiefunctie](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in het verleden (met Adobe Audience Manager of andere toepassingen), neemt u contact op met Adobe Consulting of Customer Care om ID-syncs in te schakelen. Als u al eerder was ingesteld [!DNL Microsoft Bing] Als u integreert in Audience Manager, worden de id-syncs die u hebt ingesteld, overgedragen naar Platform.

Wanneer het vormen van de bestemming, moet u de volgende informatie verstrekken:

* [!UICONTROL Account ID]: dit is uw [!DNL Bing Ads CID], in geheel-getalnotatie.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL Bing Ads CID].

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

In de [Segmentatieschema](../../ui/activate-segment-streaming-destinations.md#scheduling) stap, moet u uw segmenten aan hun overeenkomstige identiteitskaart of vriendschappelijke naam in de bestemming manueel in kaart brengen.

Wanneer het in kaart brengen van segmenten, adviseren wij u gebruiken [!DNL Platform] segmentnaam of een kortere vorm ervan, voor gebruiksgemak. Nochtans, te hoeven segmentidentiteitskaart of de naam in uw bestemming niet om in te passen in uw [!DNL Platform] account. Elke waarde die u in het toewijzingsveld invoegt, wordt weerspiegeld door het doel.

## Geëxporteerde gegevens {#exported-data}

Controleren of gegevens zijn geëxporteerd naar de [!DNL Microsoft Bing] doel, controleer uw [!DNL Microsoft Bing Ads] account. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.
