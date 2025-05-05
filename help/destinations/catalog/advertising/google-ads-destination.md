---
title: Google Ads-verbinding
description: Google Ads, voorheen bekend als Google AdWords, is een online advertentieservice waarmee bedrijven per klik reclame kunnen betalen voor zoekopdrachten, grafische weergaven, YouTube-video's en mobiele displays in de app.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# [!DNL Google Ads] verbinding

## Overzicht {#overview}

[!DNL Google Ads], voorheen bekend als [!DNL Google AdWords] , is een onlinereclame waarmee bedrijven per klik reclame kunnen betalen voor zoekopdrachten op basis van tekst, grafische weergaven, [!DNL YouTube] video&#39;s en mobiele weergaven in de app.

## Doelspecificaties {#specifics}

Let op de volgende details die specifiek zijn voor [!DNL Google Ads] doelen:

* Geactiveerd publiek wordt programmatically gecreeerd in het [!DNL Google] platform.
* [!DNL Experience Platform] bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg het aantal gebruikers in Google om de integratie te valideren en te begrijpen waar de doelgroep zich op richt.

>[!IMPORTANT]
>
>Als u uw eerste bestemming met [!DNL Google Ads] wilt tot stand brengen en niet de [ functionaliteit van de Synchronisatie van identiteitskaart ](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=nl-NL) in de Dienst van identiteitskaart van Experience Cloud in het verleden (met Audience Manager of andere toepassingen) hebt toegelaten, bereik uit aan Adobe Consulting of de Zorg van de Klant om de syncs van identiteitskaart toe te laten. Als u eerder Google-integratie hebt ingesteld in Audience Manager, worden de id-syncs die u hebt ingesteld, overgedragen naar Experience Platform.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Google Ads] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Selecteer deze doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | [!DNL Apple ID for Advertisers] | Selecteer deze doelidentiteit wanneer uw bronidentiteit een IDFA-naamruimte is. |
| AAM UUID | [ Adobe Audience Manager  [!DNL Unique User ID] ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=nl-NL), ook gekend als [!DNL Device ID]. Een numerieke, 38-cijferige apparaat-id die Audience Manager koppelt aan elk apparaat waarmee het werkt. | Google gebruikt [ AAM UUID ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=nl-NL) aan doelgebruikers in Californië, en identiteitskaart van de Koekje van Google voor alle andere gebruikers. |
| [!DNL Google] cookie-id | [!DNL Google] cookie-id | [!DNL Google] gebruikt deze id om gebruikers buiten Californië als doel in te stellen. |
| RIDA | Roku-id voor Advertising. Deze id identificeert unieke Roku-apparaten. |  |
| GEMAAKT | Microsoft Advertising ID. Deze id identificeert apparaten waarop Windows 10 wordt uitgevoerd op unieke wijze. |  |
| Amazon Fire TV ID | Deze id is uniek voor Amazon Fire TV&#39;s. |  |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek naar de Google-bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

### Bestaande [!DNL Google Ads] account

>[!IMPORTANT]
>
> [!DNL Google] heeft de nieuwe [!DNL Google Ads] cookie-integratie met externe leveranciers vervangen. Als u de stappen voor lijst van gewenste personen in de volgende sectie wilt uitvoeren, moet u over een bestaande integratie met [!DNL Google Ads] beschikken. Het instellen van een [!DNL Google Customer Match] -integratie wordt daarom aanbevolen voor het gebruik van [!DNL Google Ads] . Lees de zelfstudie over het maken van een [[!DNL Google Customer Match]](./google-customer-match.md) -verbinding voor meer informatie over het maken van een [!DNL Google Customer Match] -integratie.

### Aanbieding toestaan {#allow-listing}

>[!NOTE]
>
>Aanbieding toestaan is verplicht voordat u de eerste [!DNL Google Ads] -bestemming in Experience Platform instelt. Zorg ervoor dat het hieronder beschreven proces voor het aanbieden van objecten in een aanbieding door [!DNL Google] is voltooid voordat u een bestemming maakt.
>De uitzondering op deze regel is voor [ Audience Manager ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=nl-NL) klanten. Als je al een verbinding met deze Google-bestemming in Audience Manager hebt gemaakt, hoeft je het proces voor het aanbieden van objecten in de lijst niet opnieuw te doorlopen en kunt je doorgaan met de volgende stappen.

Voordat u de [!DNL Google Ads] -bestemming maakt in Experience Platform, moet u contact opnemen met [!DNL Google] om Adobe op te nemen in de lijst met toegestane gegevensproviders en om uw account toe te voegen aan de lijst van gewenste personen. Neem contact op met [!DNL Google] en geef de volgende informatie op:

* **identiteitskaart van de Rekening**: De rekeningidentiteitskaart van Adobe met Google. Account-ID: 87933855.
* **identiteitskaart van de Klant**: De identiteitskaart van de Klant van Adobe met Google. Klant-id: 89690775.
* Uw accounttype: **AdWords**
* **identiteitskaart van Google AdWords**: Dit is uw identiteitskaart met [!DNL Google]. De id-indeling heeft doorgaans de notatie 123-456-7890.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [ vestiging ](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Account Type]**: AdWords is de enige beschikbare optie.
* **[!UICONTROL Account ID]**: vul uw account-id in met [!DNL Google Ads] . De id-indeling heeft doorgaans de notatie 123-456-7890.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Zie [ publieksgegevens aan het stromen publiek de uitvoerbestemmingen ](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

## Geëxporteerde gegevens

Controleer uw [!DNL Google Ads] -account om te controleren of gegevens naar de [!DNL Google Ads] -bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.

## Problemen oplossen {#troubleshooting}

### 400 Onjuist aanvraagfoutbericht {#bad-request}

Wanneer het vormen van deze bestemming, kunt u de volgende fout ontvangen:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Deze fout komt of voor wanneer de klantenrekeningen niet aan de [ eerste vereisten ](#prerequisites) voldoen of wanneer de klanten proberen om de bestemming zonder een bestaande [!DNL Google Ads] rekening te vormen.

[!DNL Google] heeft de nieuwe [!DNL Google Ads] cookie-integratie met externe leveranciers vervangen. Om de [ lijst van gewenste personen ](#allow-listing) stappen uit te voeren, moet u bestaande integratie met [!DNL Google Ads] hebben.

De aanbevolen methode voor het gebruik van [!DNL Google Ads] is het instellen van een [[!DNL Google Customer Match]](google-customer-match.md) -integratie.
