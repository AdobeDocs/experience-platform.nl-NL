---
title: Google Display & Video 360-verbinding
description: Display & Video 360, voorheen bekend als DoubleClick Bodmanager, is een hulpmiddel dat wordt gebruikt om herrichtings- en doelgerichte digitale campagnes uit te voeren in verschillende bronnen voor weergave, video en mobiele inventaris.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 3%

---

# [!DNL Google Display & Video 360]-verbinding

>[!IMPORTANT]
>
> Google geeft veranderingen in de [&#x200B; Adds API van Google &#x200B;](https://developers.google.com/google-ads/api/docs/start), [&#x200B; Overeenkomst van de Klant &#x200B;](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) vrij, en [&#x200B; Vertoning &amp; Video 360 API &#x200B;](https://developers.google.com/display-video/api/guides/getting-started/overview) om de naleving en toestemmingsgerelateerde vereisten te steunen die onder de [&#x200B; Wet van de Markten &#x200B;](https://digital-markets-act.ec.europa.eu/index_nl) (DMA) worden bepaald in de Europese Unie ([&#x200B; het Beleid van de Toestemming van de Gebruiker EU &#x200B;](https://www.google.com/about/company/user-consent-policy/)). De handhaving van deze wijzigingen in de toestemmingsvereisten is vanaf 6 maart 2024 van kracht.
><br/>
>Om zich aan het EU-beleid inzake instemming van gebruikers te houden en door te gaan met het opstellen van publiekslijsten voor gebruikers in de Europese Economische Ruimte (EER), moeten adverteerders en partners ervoor zorgen dat zij toestemming van de eindgebruiker geven bij het uploaden van publieksgegevens. Als Google-partner beschikt Adobe over de benodigde tools om te voldoen aan deze toestemmingsvereisten in het kader van de DMA in de Europese Unie.
><br/>
>De klanten die de Privacy &amp; het Schild van de Veiligheid van Adobe hebben gekocht en het beleid van de a [&#x200B; toestemming &#x200B;](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) gevormd om niet-goedgekeurde profielen uit te filteren hoeven geen actie te ondernemen.
><br/>
>De klanten die geen de Privacy &amp; het Schild van de Veiligheid van Adobe hebben gekocht moeten de [&#x200B; mogelijkheden van de segmentdefinitie &#x200B;](../../../segmentation/home.md#segment-definitions) binnen [&#x200B; de Bouwer van het Segment &#x200B;](../../../segmentation/ui/segment-builder.md) aan filter uit niet-goedgekeurde profielen gebruiken, om de bestaande bestemmingen van Real-Time CDP Google zonder onderbreking te blijven gebruiken.

[!DNL Display & Video 360] (voorheen bekend als [!DNL DoubleClick Bid Manager] ) is een programma waarmee u doelgerichte digitale campagnes voor weergave, video en mobiele inventarisbronnen kunt uitvoeren.

## Doelspecificaties {#specifics}

Let op de volgende details die specifiek zijn voor [!DNL Google Display & Video 360] doelen:

* Geactiveerd publiek wordt programmatically gecreeerd in het platform van Google.
* De activering van publieksbackfills naar de [!DNL Google Display & Video 360] -bestemming vindt plaats 24-48 uur nadat een publiek voor het eerst is toegewezen aan een doelverbinding. Deze update is een reactie op het Google-beleid om 24 uur te wachten tot er gegevens zijn ingevoerd. De update is bedoeld om de overeenkomende snelheden tussen Real-Time CDP en [!DNL Google Display & Video 360] te verbeteren. Dit is een achtergrondconfiguratie die op deze bestemming slechts van toepassing is en die niet met om het even welke klant-configureerbare het plannen opties in UI verwant is.

>[!IMPORTANT]
>
>Als u uw eerste bestemming met de Vertoning van Google &amp; Video 360 wilt tot stand brengen en niet de [&#x200B; functionaliteit van de Synchronisatie van identiteitskaart &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in de Dienst van identiteitskaart van Experience Cloud in het verleden (met Adobe Audience Manager of andere toepassingen) hebben toegelaten, bereik uit aan Adobe Consulting of de Zorg van de Klant om de syncs van identiteitskaart toe te laten. Als u eerder Google-integratie hebt ingesteld in Audience Manager, worden de id-syncs die u hebt ingesteld, overgedragen naar Experience Platform.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Google Display & Video 360] ondersteunt de activering van soorten publiek op basis van de identiteiten in de onderstaande tabel. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Identiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [&#x200B; Adobe Audience Manager  [!DNL Unique User ID] &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), ook gekend als [!DNL Device ID]. Een numerieke, 38-cijferige apparaat-id die Audience Manager koppelt aan elk apparaat waarmee het werkt. | Google gebruikt [&#x200B; AAM UUID &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) aan doelgebruikers in Californië, en identiteitskaart van de Koekje van Google voor alle andere gebruikers. |
| [!DNL Google] cookie-id | [!DNL Google] cookie-id | [!DNL Google] gebruikt deze id om gebruikers buiten Californië als doel in te stellen. |
| RIDA | Roku-id voor Advertising. Deze id identificeert unieke Roku-apparaten. |  |
| GEMAAKT | Microsoft Advertising ID. Deze id identificeert apparaten waarop Windows 10 wordt uitgevoerd op unieke wijze. |  |
| Amazon Fire TV ID | Deze id is uniek voor Amazon Fire TV&#39;s. |  |

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Alle andere doelgroepen | Ja | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [&#x200B; diverse publieksoorsprong &#x200B;](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-apps, zoals Adobe Journey Optimizer; </li><li> en meer. </li></ul> |

{style="table-layout:auto"}



Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
|--------------------|-----------|-------------|-----------|
| [&#x200B; het publiek van Mensen &#x200B;](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [&#x200B; publiek van de Rekening &#x200B;](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [&#x200B; Het publiek van het Vooruitzicht &#x200B;](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [&#x200B; de uitvoer van de Dataset &#x200B;](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het Data Lake van Adobe Experience Platform. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}


## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek naar de Google-bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

## Vereisten {#prerequisites}

### Aanbieding toestaan {#allow-listing}

>[!NOTE]
>
>Aanbieding toestaan is verplicht voordat u de eerste [!DNL Google Display & Video 360] -bestemming in Experience Platform instelt. Controleer of het hieronder beschreven proces voor het aanbieden van een geldige aanbieding door [!DNL Google] is voltooid voordat u een bestemming maakt.
>De uitzondering op deze regel is voor [&#x200B; Audience Manager &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) klanten. Als je al een verbinding met deze Google-bestemming in Audience Manager hebt gemaakt, hoeft je het proces voor het aanbieden van objecten in de lijst niet opnieuw te doorlopen en kunt je doorgaan met de volgende stappen.

Voordat u de [!DNL Google Display & Video 360] -bestemming maakt in Experience Platform, moet u contact opnemen met Google om Adobe op te nemen in de lijst met toegestane gegevensproviders en om uw account toe te voegen aan de lijst van gewenste personen. Neem contact op met Google en geef de volgende informatie op:

* **identiteitskaart van de Rekening**: De rekeningidentiteitskaart van Adobe met Google. Account-ID: 87933855.
* **identiteitskaart van de Klant**: De identiteitskaart van de Klant van Adobe met Google. Klant-id: 89690775.
* **Uw accounttype**: gebruik **[!DNL Invite advertiser]** om publiek toe te staan om slechts aan een specifiek merk in uw Vertoning &amp; Video 360 rekening worden gedeeld of gebruik **[!DNL Invite partner]** om publiek toe te staan om aan alle merken in uw Vertoning &amp; Video 360 rekening worden gedeeld.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [&#x200B; vestiging &#x200B;](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Account Type]**: Selecteer een optie, afhankelijk van uw account bij Google:
   * Gebruik `Invite Advertiser` om het publiek alleen te laten delen naar een specifiek merk in uw Display &amp; Video 360-account.
   * Gebruik `Invite Partner` om het publiek toe te staan om aan alle merken in uw Vertoning &amp; Video 360 rekening worden gedeeld.
* **[!UICONTROL Account ID]**: vul uw **[!DNL Invite partner]** - of **[!DNL Invite advertiser]** account-id in met Google. Dit is doorgaans een ID van zes of zeven cijfers.

>[!NOTE]
>
>Wanneer u een [!DNL Google Display & Video 360] -bestemming instelt, werkt u samen met uw [!DNL Google Account Manager] - of Adobe-vertegenwoordiger om te weten welk accounttype u hebt.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Zie [&#x200B; publieksgegevens aan het stromen publiek de uitvoerbestemmingen &#x200B;](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Google Display & Video 360] -account om te controleren of gegevens naar de [!DNL Google Display & Video 360] -bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.

## Problemen oplossen {#troubleshooting}

### 400 Onjuist aanvraagfoutbericht {#bad-request}

Wanneer het vormen van deze bestemming, kunt u de volgende fout ontvangen:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Deze fout komt voor wanneer de klantenrekeningen niet aan de [&#x200B; eerste vereisten &#x200B;](#prerequisites) voldoen. Neem contact op met Google om dit probleem op te lossen en zorg ervoor dat je account op de lijst staat.