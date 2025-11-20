---
keywords: google en manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google en manager; DFP
title: Google Ad Manager-verbinding
description: Google Ad Manager, voorheen bekend als DoubleClick voor Publishers of DoubleClick AdX, is een advertentieplatform uit Google dat uitgevers de mogelijkheid biedt om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 3%

---

# [!DNL Google Ad Manager]-verbinding

>[!IMPORTANT]
>
> Google geeft veranderingen in de [&#x200B; Adds API van Google &#x200B;](https://developers.google.com/google-ads/api/docs/start), [&#x200B; Overeenkomst van de Klant &#x200B;](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) vrij, en [&#x200B; Vertoning &amp; Video 360 API &#x200B;](https://developers.google.com/display-video/api/guides/getting-started/overview) om de naleving en toestemmings-gerelateerde vereisten te steunen die onder de [&#x200B; Wet van de Markten &#x200B;](https://digital-markets-act.ec.europa.eu/index_nl) (DMA) worden bepaald in de Europese Unie ([&#x200B; EU het Beleid van de Toestemming van de Gebruiker &#x200B;](https://www.google.com/about/company/user-consent-policy/)). De handhaving van deze wijzigingen in de toestemmingsvereisten is vanaf 6 maart 2024 van kracht.
><br/>
>Om zich aan het EU-beleid inzake instemming van gebruikers te houden en door te gaan met het opstellen van publiekslijsten voor gebruikers in de Europese Economische Ruimte (EER), moeten adverteerders en partners ervoor zorgen dat zij toestemming van de eindgebruiker geven bij het uploaden van publieksgegevens. Als Google-partner beschikt Adobe over de benodigde tools om te voldoen aan deze toestemmingsvereisten in het kader van de DMA in de Europese Unie.
><br/>
>De klanten die de Privacy &amp; het Schild van de Veiligheid van Adobe hebben gekocht en het beleid van de a [&#x200B; toestemming &#x200B;](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) gevormd om niet-goedgekeurde profielen uit te filteren hoeven geen actie te ondernemen.
><br/>
>De klanten die geen de Privacy &amp; het Schild van de Veiligheid van Adobe hebben gekocht moeten de [&#x200B; mogelijkheden van de segmentdefinitie &#x200B;](../../../segmentation/home.md#segment-definitions) binnen [&#x200B; de Bouwer van het Segment &#x200B;](../../../segmentation/ui/segment-builder.md) aan filter uit niet-goedgekeurde profielen gebruiken, om de bestaande bestemmingen van Real-Time CDP Google zonder onderbreking te blijven gebruiken.


[!DNL Google Ad Manager], voorheen bekend als [!DNL DoubleClick for Publishers] (DFP) of [!DNL DoubleClick AdX] , is een platform voor advertentie in [!DNL Google] dat uitgevers de mogelijkheid biedt om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren.

## Doelspecificaties {#specifics}

Let op de volgende details die specifiek zijn voor [!DNL Google Ad Manager] doelen:

* Geactiveerd publiek wordt programmatically gecreeerd in het [!DNL Google] platform.
* [!DNL Experience Platform] bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg het aantal gebruikers in Google om de integratie te valideren en te begrijpen waar de doelgroep zich op richt.
* Nadat u een publiek hebt toegewezen aan een [!DNL Google Ad Manager] -doel, wordt de publieksnaam direct weergegeven in de gebruikersinterface van [!DNL Google Ad Manager] .
* De segmentpopulatie moet 24-48 uur in [!DNL Google Ad Manager] worden weergegeven. Bovendien moeten doelgroepen een publieksgrootte hebben van ten minste 50 profielen om te kunnen worden weergegeven in [!DNL Google Ad Manager] . Soorten publiek met een grootte kleiner dan 50 profielen worden niet ingevuld in [!DNL Google Ad Manager] .

## Ondersteunde identiteiten {#supported-identities}

[!DNL Google Ad Manager] ondersteunt de activering van soorten publiek op basis van de identiteiten in de onderstaande tabel. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Identiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [&#x200B; Adobe Audience Manager  [!DNL Unique User ID] &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=nl-NL), ook gekend als [!DNL Device ID]. Een numerieke, 38-cijferige apparaat-id die Audience Manager koppelt aan elk apparaat waarmee het werkt. | Google gebruikt [&#x200B; AAM UUID &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=nl-NL) aan doelgebruikers in Californië, en identiteitskaart van de Koekje van Google voor alle andere gebruikers. |
| [!DNL Google] cookie-id | [!DNL Google] cookie-id | [!DNL Google] gebruikt deze id om gebruikers buiten Californië als doel in te stellen. |
| RIDA | Roku-id voor Advertising. Deze id identificeert unieke Roku-apparaten. |  |
| GEMAAKT | Microsoft Advertising ID. Deze id identificeert apparaten waarop Windows 10 wordt uitgevoerd op unieke wijze. |  |
| Amazon Fire TV ID | Deze id is uniek voor Amazon Fire TV&#39;s. |  |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek naar de Google-bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

Als u uw eerste bestemming met [!DNL Google Ad Manager] wilt tot stand brengen en niet de [&#x200B; functionaliteit van de Synchronisatie van identiteitskaart &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=nl-NL) in de Dienst van identiteitskaart van Experience Cloud in het verleden (met Audience Manager of andere toepassingen) hebt toegelaten, te bereiken gelieve uit aan Adobe Consulting of de Zorg van de Klant om de syncs van identiteitskaart toe te laten. Als u eerder [!DNL Google] -integraties hebt ingesteld in Audience Manager, worden de id-syncs die u hebt ingesteld, overgedragen naar Experience Platform.

### Aanbieding toestaan {#allow-listing}

Aanbieding toestaan is verplicht voordat u de eerste [!DNL Google Ad Manager] -bestemming in Experience Platform instelt. Voltooi de hieronder beschreven procedure voor het aanbieden van objecten in een geldige plaats voordat je de bestemming maakt.

1. Volg de stappen in [&#x200B; worden beschreven Google en de documentatie van de Manager &#x200B;](https://support.google.com/admanager/answer/3289669?hl=en) om Adobe als verbonden Platform van het Beheer van Gegevens toe te voegen (DMP) die.
2. Ga in de interface [!DNL Google Ad Manager] naar **[!UICONTROL Admin]** > **[!UICONTROL Global Settings]** > **[!UICONTROL Network Settings]** en schakel de schuifregelaar **[!UICONTROL API Access]** in.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Id van publiek toevoegen aan publieksnaam"
>abstract="Selecteer deze optie als u de volgende gebruikers-id uit Experience Platform wilt laten opnemen in de naam van het publiek in Google Ad Manager: `Audience Name (Audience ID)`"

Terwijl [&#x200B; vestiging &#x200B;](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Account ID]**: voer uw [!DNL Audience Link ID] vanuit uw [!DNL Google] account in. Dit is een specifieke id die is gekoppeld aan uw [!DNL Google Ad Manager] -netwerk (niet aan uw [!DNL Network code] ). U vindt dit onder **[!UICONTROL Admin > Global settings]** in de [!DNL Google Ad Manager] -interface.
* **[!UICONTROL Account Type]**: Selecteer een optie, afhankelijk van uw account bij Google:
   * `DFP by Google` gebruiken voor [!DNL DoubleClick] voor uitgevers
   * `AdX buyer` gebruiken voor [!DNL Google AdX]
* **[!UICONTROL Append audience ID to audience name]**: Selecteer deze optie als u in Google Ad Manager de gebruikers-id van Experience Platform wilt opnemen, bijvoorbeeld: `Audience Name (Audience ID)` .

>[!NOTE]
>
>Wanneer u een [!DNL Google Ad Manager] -bestemming instelt, werkt u samen met uw [!DNL Google Account Manager] - of Adobe-vertegenwoordiger om te weten welk accounttype u hebt.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Zie [&#x200B; publieksgegevens aan het stromen publiek de uitvoerbestemmingen &#x200B;](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Google Ad Manager] -account om te controleren of gegevens naar de [!DNL Google Ad Manager] -bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.

## Problemen oplossen {#troubleshooting}

Als u tijdens het gebruik van dit doel fouten tegenkomt en naar Adobe of Google moet reiken, moet u de volgende id&#39;s bij de hand houden.

Dit zijn Adobe Google-account-id&#39;s:

* **[!UICONTROL Account ID]**: 87933855
* **[!UICONTROL Customer ID]**: 89690775