---
keywords: 'reclame; borden; '
title: Microsoft Bing-verbinding
description: Met de de verbindingsbestemming van de Bing van Microsoft, kunt u het opnieuw richten en publiek gerichte digitale campagnes over de Reclame van de Vertoning van Microsoft uitvoeren.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 1%

---

# [!DNL Microsoft Bing] verbinding {#bing-destination}

## Overzicht {#overview}

Met de bestemming [!DNL Microsoft Bing] kunt u profielgegevens naar [!DNL Microsoft Display Advertising] verzenden.

Als u profielgegevens naar [!DNL Microsoft Bing] wilt verzenden, moet u eerst verbinding maken met het doel.

## Gebruiksscenario’s {#use-cases}

Als markator, wil ik segmenten kunnen gebruiken die van [!DNL Microsoft Advertising IDs] worden gebouwd om gebruikers door vertoningsreclame over [!DNL Microsoft Advertising] kanalen te richten.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Microsoft Bing] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|---|
| GEMAAKT | Microsoft Advertising ID |

## Exporttype {#export-type}

**[!DNL Segment Export]** - u exporteert alle leden van een segment (publiek) naar de  [!DNL Microsoft Bing] bestemming.

## Vereisten {#prerequisites}

Als u uw eerste bestemming met [!DNL Microsoft Bing] wilt maken en in het verleden (met Adobe Audience Manager of andere toepassingen) de [ID-synchronisatiefunctionaliteit](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) niet hebt ingeschakeld in de Experience Cloud ID-service, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder [!DNL Microsoft Bing] integraties in Audience Manager had opgezet, de syncs van identiteitskaart u opstelling dragen over aan Platform.

Wanneer het vormen van de bestemming, moet u de volgende informatie verstrekken:

* [!UICONTROL Account ID]: Dit is uw  [!DNL Bing Ads CID]geheel getal.

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL Bing Ads CID].

## Segmenten naar dit doel activeren {#activate}

Zie [Profielen en segmenten activeren aan een doel](../../ui/activate-destinations.md) voor instructies bij het activeren van publiekssegmenten aan bestemmingen.

In [Segmentprogramma](../../ui/activate-destinations.md#segment-schedule) stap, moet u uw segmenten aan hun overeenkomstige identiteitskaart of vriendschappelijke naam in de bestemming manueel in kaart brengen.

Wanneer het in kaart brengen van segmenten, adviseren wij u de [!DNL Platform] segmentnaam of een kortere vorm van het, voor gemak van gebruik te gebruiken. Nochtans, te hoeven segmentidentiteitskaart of de naam in uw bestemming niet om in uw [!DNL Platform] rekening aan te passen. Elke waarde die u in het toewijzingsveld invoegt, wordt weerspiegeld door het doel.

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Microsoft Bing Ads]-account om te controleren of gegevens naar de [!DNL Microsoft Bing]-bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.
