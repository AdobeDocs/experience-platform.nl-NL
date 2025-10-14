---
title: (Beta)  [!DNL Google Ad Manager 360]  verbinding
description: Google Ad Manager 360 is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 3%

---

# (Beta) [!DNL Google Ad Manager 360] -verbinding

>[!IMPORTANT]
>
> Google geeft veranderingen in de [&#x200B; Adds API van Google &#x200B;](https://developers.google.com/google-ads/api/docs/start), [&#x200B; Overeenkomst van de Klant &#x200B;](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) vrij, en [&#x200B; Vertoning &amp; Video 360 API &#x200B;](https://developers.google.com/display-video/api/guides/getting-started/overview) om de naleving en toestemmings-gerelateerde vereisten te steunen die onder de [&#x200B; Wet van de Markten &#x200B;](https://digital-markets-act.ec.europa.eu/index_nl) (DMA) worden bepaald in de Europese Unie ([&#x200B; EU het Beleid van de Toestemming van de Gebruiker &#x200B;](https://www.google.com/about/company/user-consent-policy/)). De handhaving van deze wijzigingen in de toestemmingsvereisten is vanaf 6 maart 2024 van kracht.
><br/>
>Om zich aan het EU-beleid inzake instemming van gebruikers te houden en door te gaan met het opstellen van publiekslijsten voor gebruikers in de Europese Economische Ruimte (EER), moeten adverteerders en partners ervoor zorgen dat zij toestemming van de eindgebruiker geven bij het uploaden van publieksgegevens. Als Google-partner beschikt Adobe over de benodigde tools om te voldoen aan deze toestemmingsvereisten in het kader van de DMA in de Europese Unie.
><br/>
>De klanten die de Privacy &amp; het Schild van de Veiligheid van Adobe hebben gekocht en het beleid van de a [&#x200B; toestemming &#x200B;](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) gevormd om niet-goedgekeurde profielen uit te filteren hoeven geen actie te ondernemen.
><br/>
>De klanten die geen de Privacy &amp; het Schild van de Veiligheid van Adobe hebben gekocht moeten de [&#128279;](../../../segmentation/home.md#segment-definitions) mogelijkheden van de segmentdefinitie  binnen [&#x200B; de Bouwer van het Segment &#x200B;](../../../segmentation/ui/segment-builder.md) aan filter uit niet-goedgekeurde profielen gebruiken, om de bestaande bestemmingen van Real-Time CDP Google zonder onderbreking te blijven gebruiken.

Met de [!DNL Google Ad Manager 360] -verbinding kunt u via [!DNL Google Cloud Storage] batchupload uitvoeren naar [!DNL publisher provided identifiers] (PPID) [!DNL Google Ad Manager 360] .

Voor meer details op hoe de uitgever verstrekte herkenningstekens in Manager 360 van Google en Advertentie werkte, zie de [&#x200B; officiële documentatie van Google &#x200B;](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Deze bestemming is momenteel in Beta en is slechts beschikbaar voor een beperkt aantal klanten. Als u toegang tot de [!DNL Google Ad Manager 360] -verbinding wilt aanvragen, neemt u contact op met uw Adobe-vertegenwoordiger en geeft u [!DNL organization ID] op.

De [!DNL Google Ad Manager 360] -bestemming exporteert [!DNL CSV] -bestanden naar uw [!DNL Google Cloud Storage] -emmertje. Nadat u de [!DNL CSV] -bestanden hebt geëxporteerd, moet u deze importeren in uw [!DNL Google Ad Manager 360] -account.

## Doelspecificaties {#specifics}

Let op de volgende details die specifiek zijn voor [!DNL Google Ad Manager 360] doelen.

* Deze bestemming steunt momenteel niet de [&#x200B; de uitvoerdossiers op bestelling &#x200B;](../../ui/export-file-now.md) eigenschap.
* Geactiveerd publiek wordt met programmacode gemaakt in het Google-platform en gevuld in het CSV-bestand.

## Ondersteunde identiteiten {#supported-identities}

[!DNL This integration] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Selecteer deze doelidentiteit om het publiek naar [!DNL Google Ad Manager 360] te sturen |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de toepasselijke schemagebieden (bijvoorbeeld uw PPID), zoals gekozen in het scherm van de uitgezochte profielkenmerken van het [&#x200B; werkschema van de bestemmingsactivering &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [&#x200B; partij op dossier-gebaseerde bestemmingen &#x200B;](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

### Aanbieding toestaan {#allow-listing}

Aanbieding toestaan is verplicht voordat u de eerste [!DNL Google Ad Manager 360] -bestemming in Experience Platform instelt. Voltooi de hieronder beschreven procedure voor het aanbieden van objecten in een geldige plaats voordat je de bestemming maakt.

>[!NOTE]
>
>De uitzondering op deze regel is voor bestaande [&#x200B; Audience Manager &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=nl-NL) klanten. Als je al een verbinding met deze Google-bestemming in Audience Manager hebt gemaakt, hoeft je het proces voor het aanbieden van objecten in de lijst niet opnieuw te doorlopen en kunt je doorgaan met de volgende stappen.

1. Volg de stappen in [&#x200B; worden beschreven Google en de documentatie van de Manager &#x200B;](https://support.google.com/admanager/answer/3289669?hl=en) om Adobe als verbonden Platform van het Beheer van Gegevens toe te voegen (DMP) die.
2. Ga in de interface [!DNL Google Ad Manager] naar **[!UICONTROL Admin]** > **[!UICONTROL Global Settings]** > **[!UICONTROL Network Settings]** en schakel de schuifregelaar **[!UICONTROL API Access]** in.


## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=nl-NL) worden beschreven. Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

* **[!UICONTROL Access key ID]**: Een alfanumerieke tekenreeks van 61 tekens die wordt gebruikt om uw [!DNL Google Cloud Storage] -account te verifiëren bij Experience Platform.
* **[!UICONTROL Secret access key]**: Een tekenreeks met een basiscode van 40 tekens die wordt gebruikt om uw [!DNL Google Cloud Storage] -account te verifiëren bij Experience Platform.

Voor meer informatie over deze waarden, zie de [&#x200B; de sleutels van HMAC van de Opslag van de Wolk van Google HMAC &#x200B;](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) gids. Voor stappen op hoe te om uw eigen toegangs zeer belangrijke identiteitskaart en geheime toegangssleutel te produceren, verwijs naar het [[!DNL Google Cloud Storage]  bronoverzicht &#x200B;](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="Id van publiek toevoegen aan publieksnaam"
>abstract="Selecteer deze optie als u de publieksnaam in deze bestemming als volgt wilt laten weergeven met de gebruikers-id uit Experience Platform: `Audience Name (Audience ID)`"

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Folder path]**: voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL Bucket name]**: voer de naam in van het [!DNL Google Cloud Storage] emmertje dat door dit doel moet worden gebruikt.
* **[!UICONTROL Account ID]**: voer uw [!DNL Audience Link ID] vanuit uw [!DNL Google] account in. Dit is een specifieke id die is gekoppeld aan uw [!DNL Google Ad Manager] -netwerk (niet aan uw [!DNL Network code] ). U vindt dit onder **[!UICONTROL Admin > Global settings]** in de [!DNL Google Ad Manager] -interface.
* **[!UICONTROL Account Type]**: Selecteer een optie, afhankelijk van uw [!DNL Google] -account:
   * `AdX buyer` gebruiken voor [!DNL Google AdX]
   * `DFP by Google` gebruiken voor [!DNL DoubleClick] voor uitgevers
* **[!UICONTROL Append audience ID to audience name]**: Selecteer deze optie als u in Google Ad Manager 360 de gebruikers-id van Experience Platform wilt opnemen, zoals in dit voorbeeld: `Audience Name (Audience ID)` .

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [&#x200B; publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](../../ui/activate-batch-profile-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

In de stap voor identiteitstoewijzing kunt u de volgende vooraf ingevulde toewijzingen zien:

| Vooraf ingevulde toewijzing | Beschrijving |
|---------|----------|
| `ECID` -> `ppid` | Dit is de enige door de gebruiker bewerkbare vooraf ingevulde toewijzing. U kunt al uw kenmerken of naamruimten selecteren in Experience Platform en deze toewijzen aan `ppid` . |
| `metadata.segment.alias` -> `list_id` | Hiermee wijst u Experience Platform-publieksnamen toe aan gebruikers-id&#39;s in het Google-platform. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Vertelt het Google-platform wanneer gediskwalificeerde gebruikers uit segmenten moeten worden verwijderd. |

Deze toewijzingen zijn vereist door [!DNL Google Ad Manager 360] en worden automatisch door Adobe Experience Platform gemaakt voor alle [!DNL Google Ad Manager 360] -verbindingen.

![&#x200B; beeld UI die de afbeeldingsstap voor Manager 360 van de Advertentie van Google toont.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Geëxporteerde gegevens {#exported-data}

Om te controleren of gegevens zijn geëxporteerd, controleert u het emmertje van [!DNL Google Cloud Storage] en controleert u of de geëxporteerde bestanden de verwachte profielpopulaties bevatten.

## Problemen oplossen {#troubleshooting}

Als u tijdens het gebruik van dit doel fouten tegenkomt en naar Adobe of Google moet reiken, moet u de volgende id&#39;s bij de hand houden.

Dit zijn Adobe Google-account-id&#39;s:

* **[!UICONTROL Account ID]**: 87933855
* **[!UICONTROL Customer ID]**: 89690775