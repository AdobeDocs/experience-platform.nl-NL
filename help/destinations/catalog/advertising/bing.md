---
keywords: reclame; banden;
title: Microsoft Bing-verbinding
description: Met de bestemming van de Microsoft Bing-verbinding kunt u gerichte digitale campagnes opnieuw richten en publieksgericht voeren op het gehele Microsoft Advertising-netwerk, waaronder Weergaveadvertenties, Zoeken en Native.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: b282dbae9131e0d2acdcd999d57f2e08b0bd7810
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 1%

---

# [!DNL Microsoft Bing]-verbinding {#bing-destination}

## Overzicht {#overview}


>[!IMPORTANT]
>
>Na een interne verbetering aan de bestemmingsdienst van Augustus 2025, kunt u a **daling in het aantal geactiveerde profielen** in uw dataflows [!DNL Microsoft Bing] ervaren.
>
> Dit daling wordt veroorzaakt door de introductie van het **ECID afbeeldingsvereiste** voor alle activiteiten aan dit bestemmingsplatform. Zie de [&#x200B; verplichte afbeelding &#x200B;](#mandatory-mappings) sectie in deze pagina voor gedetailleerde informatie.
>
>**wat veranderde:**
>
>* De afbeelding van ECID (identiteitskaart van Experience Cloud) is nu **verplicht** voor alle profielactiviteiten.
>* Profielen zonder ECID-toewijzing zullen **weggelaten worden** uit bestaande activeringsgegevens.
>
>**wat u moet doen:**
>
>* Controleer de publieksgegevens om te controleren of profielen geldige ECID-waarden hebben.
>* Controleer de activeringsgegevens om te controleren of het profiel wordt verwacht.

Gebruik de bestemming [!DNL Microsoft Bing] om profielgegevens naar de volledige [!DNL Microsoft Advertising Network], inclusief [!DNL Display Advertising] , [!DNL Search] en [!DNL Native] te verzenden.

Het doel [!DNL Microsoft Bing] maakt *[!DNL Custom Audiences]* in Microsoft. Die zijn beschikbaar zowel in [!DNL Microsoft Search Network] als [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]) zoals vermeld in de [&#x200B; documentatie van Advertising van Microsoft &#x200B;](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

Als u profielgegevens naar [!DNL Microsoft Bing] wilt verzenden, moet u eerst verbinding maken met het doel.

## Gebruiksscenario’s {#use-cases}

Als markator wil ik het publiek dat is samengesteld uit [!DNL Microsoft Advertising IDs] , kunnen gebruiken om gebruikers als doelgroep op te roepen via weergave- of zoekadvertenties langs [!DNL Microsoft Advertising] -kanalen.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Microsoft Bing] ondersteunt de activering van soorten publiek op basis van de identiteiten in de onderstaande tabel. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Identiteit | Beschrijving |
|---|---|
| GEMAAKT | MICROSOFT ADVERTISING ID |
| ECID | Experience Cloud-id. Deze identiteit is verplicht voor de integratie, maar wordt niet gebruikt voor activering van het publiek. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

**[!DNL Audience Export]** - u exporteert alle leden van een publiek naar het [!DNL Microsoft Bing] -doel.

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek naar het doel van [!DNL Microsoft Bing] . |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
>Als u uw eerste bestemming met [!DNL Microsoft Bing] wilt tot stand brengen en niet de [&#x200B; functionaliteit van de Synchronisatie van identiteitskaart &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=nl-NL) in de Dienst van identiteitskaart van Experience Cloud in het verleden (met Adobe Audience Manager of andere toepassingen) hebt toegelaten, te bereiken gelieve uit aan Adobe Consulting of de Zorg van de Klant om de syncs van identiteitskaart toe te laten. Als u eerder [!DNL Microsoft Bing] -integraties hebt ingesteld in Audience Manager, worden de id-syncs die u hebt ingesteld, overgedragen naar Experience Platform.

Wanneer het vormen van de bestemming, moet u de volgende informatie verstrekken:

* [!UICONTROL Account ID]: dit is de [!DNL Bing Ads CID] -notatie, in gehele getallen.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven.

### Doelgegevens invullen {#parameters}

Terwijl [&#x200B; vestiging &#x200B;](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL Bing Ads Customer ID] (CID). Uw CID is een geheel getal. U vindt deze in de URL wanneer u zich aanmeldt bij [!DNL Microsoft Advertising] .

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="Toewijzing-id"
>abstract="Voer de numerieke publiek-id voor de ring in waaraan u het geselecteerde segment wilt toewijzen. Als de opgegeven [!UICONTROL Mapping ID] niet overeenkomt met een gebruikers-id in de Bing-bestemming, worden de verwachte publieksgegevens in uw Bing-account niet weergegeven."

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_bing"
>title="Vooraf geconfigureerde toewijzingssets"
>abstract="Wij hebben deze twee kaartreeksen voor u vooraf gevormd. Wanneer u gegevens activeert naar Microsoft Bing, moeten de profielen die voor het geactiveerde publiek worden gekwalificeerd, ten minste een ECID-identiteit hebben die aan hun profiel is gekoppeld, om naar de bestemming te kunnen worden geëxporteerd."
>additional-url="https://experienceleague.adobe.com/nl/docs/experience-platform/destinations/catalog/advertising/bing#preconfigured-mappings" text="Lees meer over de vooraf geconfigureerde toewijzingen"

>[!IMPORTANT]
> 
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Zie [&#x200B; publieksgegevens aan het stromen publiek de uitvoerbestemmingen &#x200B;](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

In het [&#x200B; programma van het Publiek &#x200B;](../../ui/activate-segment-streaming-destinations.md#scheduling) stap, moet u de publieksnaam op het [!UICONTROL Mapping ID] gebied manueel in kaart brengen. Zo zorgt u ervoor dat de metagegevens van het publiek correct worden doorgegeven aan [!DNL Bing] .

{het beeld van 0} UI die het scherm van het publieksprogramma met een voorbeeld van toont hoe te om de publieksnaam aan Bing Mapping identiteitskaart in kaart te brengen.![](../../assets/catalog/advertising/bing/mapping-id.png)

### Verplichte toewijzingen {#mandatory-mappings}

Alle doelidentiteiten die in de [&#x200B; gesteunde identiteiten &#x200B;](#supported-identities) sectie worden beschreven zijn verplicht en moeten tijdens het proces van de publiekactivering in kaart worden gebracht. Dit omvat het volgende:

* **GEMAAKT** (identiteitskaart van Advertising van Microsoft)
* **ECID** (identiteitskaart van Experience Cloud)

Als u niet alle vereiste identiteiten toewijst, kunt u de activeringsworkflow niet voltooien. Elke identiteit dient een specifiek doel in de integratie en alle id&#39;s zijn vereist voor een correcte bestemming.

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Microsoft Bing] -account om te controleren of gegevens naar de [!DNL Microsoft Bing Ads] -bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.
