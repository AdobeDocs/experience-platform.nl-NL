---
title: (bèta) [!DNL Google Ad Manager 360] verbinding
description: Google Ad Manager 360 is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: 7d43abd507b5cee2b5c5d90af253d3e9290013a2
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 0%

---

# (bèta) [!DNL Google Ad Manager 360] verbinding

>[!IMPORTANT]
>
> Google brengt wijzigingen in de [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [Klantenovereenkomst](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)en de [Display &amp; Video 360-API](https://developers.google.com/display-video/api/guides/getting-started/overview) ter ondersteuning van de in het kader van de [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) in de Europese Unie[Beleid voor EU-gebruikerstoestemming](https://www.google.com/about/company/user-consent-policy/)). Verwacht wordt dat de handhaving van deze wijzigingen in de toestemmingsvereisten met ingang van 6 maart 2024 in werking zal treden.
><br/>
>Om zich aan het EU-beleid inzake instemming van gebruikers te houden en door te gaan met het opstellen van publiekslijsten voor gebruikers in de Europese Economische Ruimte (EER), moeten adverteerders en partners ervoor zorgen dat zij toestemming van de eindgebruiker geven bij het uploaden van publieksgegevens. Als Google-partner beschikt Adobe over de benodigde instrumenten om te voldoen aan deze toestemmingsvereisten in het kader van de DMA in de Europese Unie.
><br/>
>Klanten die een privacyschild voor Adobe hebben aangeschaft en een [toestemmingsbeleid](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) om profielen zonder toestemming uit te filteren, hoeft u geen actie te ondernemen.
><br/>
>Klanten die geen privacyschild voor Adobe hebben aangeschaft, moeten de [segmentdefinitie](../../../segmentation/home.md#segment-definitions) mogelijkheden binnen [Segment Builder](../../../segmentation/ui/segment-builder.md) om profielen zonder toestemming uit te filteren, zodat de bestaande Real-Time CDP Google-bestemmingen zonder onderbreking kunnen worden gebruikt.

De [!DNL Google Ad Manager 360] verbinding maakt batch-upload mogelijk voor [!DNL publisher provided identifiers] (PPID) in [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage].

Voor meer informatie over hoe de uitgever verstrekte herkenningstekens in Google Ad Manager 360 werkt, zie [officiële Google-documentatie](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Deze bestemming is momenteel in Bèta en is slechts beschikbaar aan een beperkt aantal klanten. Om toegang tot [!DNL Google Ad Manager 360] , neemt u contact op met uw Adobe en verstrekt u uw [!DNL organization ID].

De [!DNL Google Ad Manager 360] doelexport [!DNL CSV] bestanden naar uw [!DNL Google Cloud Storage] emmertje. Als u de [!DNL CSV] bestanden, moet u deze importeren in uw [!DNL Google Ad Manager 360] account.

## Doelspecificaties {#specifics}

Let op de volgende details die specifiek zijn voor [!DNL Google Ad Manager 360] bestemmingen.

* Geactiveerd publiek wordt met programmacode gemaakt in het Google-platform en gevuld in het CSV-bestand.

## Ondersteunde identiteiten {#supported-identities}

[!DNL This integration] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Selecteer deze doelidentiteit om het publiek naar te sturen [!DNL Google Ad Manager 360] |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de toepasselijke schemavelden (bijvoorbeeld uw PPID), zoals u hebt gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

### Aanbieding toestaan {#allow-listing}

Aanbieding toestaan is verplicht voordat je eerste aanbieding wordt ingesteld [!DNL Google Ad Manager 360] doel in Platform. Voltooi de hieronder beschreven procedure voor het aanbieden van objecten in een geldige plaats voordat je de bestemming maakt.

>[!NOTE]
>
>De uitzondering op deze regel geldt voor bestaande [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) klanten. Als je al een verbinding met deze Google-bestemming in Audience Manager hebt gemaakt, is het niet nodig om het proces voor het toestaan van aanbiedingen opnieuw te doorlopen en je kunt doorgaan met de volgende stappen.

1. Voer de stappen uit die in het dialoogvenster [Google Ad Manager-documentatie](https://support.google.com/admanager/answer/3289669?hl=en) Adobe toevoegen als een gekoppeld gegevensbeheerplatform (DMP).
2. In de [!DNL Google Ad Manager] interface, ga naar **[!UICONTROL Admin]** > **[!UICONTROL Global Settings]** > **[!UICONTROL Network Settings]** en de **[!UICONTROL API Access]** schuifregelaar


## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Access key ID]**: Een alfanumerieke tekenreeks van 61 tekens die wordt gebruikt voor het verifiëren van uw [!DNL Google Cloud Storage] account aan Platform.
* **[!UICONTROL Secret access key]**: Een tekenreeks van 40 tekens met de basiscode 64 die wordt gebruikt voor verificatie van uw [!DNL Google Cloud Storage] account aan Platform.

Voor meer informatie over deze waarden raadpleegt u de [HMAC-sleutels voor Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) hulplijn. Raadpleeg voor meer informatie over het genereren van uw eigen toegangstoets-id en geheime toegangstoets de [[!DNL Google Cloud Storage] bronoverzicht](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="Id van publiek toevoegen aan publieksnaam"
>abstract="Selecteer deze optie als u de publieksnaam in Google Ad Manager 360 de gebruikers-id uit het Experience Platform wilt laten opnemen, zoals in dit voorbeeld: `Audience Name (Audience ID)`"

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL Bucket name]**: Voer de naam in van de [!DNL Google Cloud Storage] emmer die door deze bestemming moet worden gebruikt.
* **[!UICONTROL Account ID]**: Voer uw [!DNL Audience Link ID] van uw [!DNL Google] account. Dit is een specifieke id die aan uw [!DNL Google Ad Manager] netwerk (niet uw [!DNL Network code]). U vindt dit onder **[!UICONTROL Admin > Global settings]** in de [!DNL Google Ad Manager] interface.
* **[!UICONTROL Account Type]**: Selecteer een optie, afhankelijk van uw [!DNL Google] account:
   * Gebruiken `AdX buyer` for [!DNL Google AdX]
   * Gebruiken `DFP by Google` for [!DNL DoubleClick] voor uitgevers
* **[!UICONTROL Append audience ID to audience name]**: Selecteer deze optie als u in Google Ad Manager 360 de gebruikers-id uit het Experience Platform wilt opnemen. Ga hierbij als volgt te werk: `Audience Name (Audience ID)`.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

In de stap voor identiteitstoewijzing kunt u de volgende vooraf ingevulde toewijzingen zien:

| Vooraf ingevulde toewijzing | Beschrijving |
|---------|----------|
| `ECID` -> `ppid` | Dit is de enige door de gebruiker bewerkbare vooraf ingevulde toewijzing. U kunt al uw kenmerken of naamruimten selecteren in Platform en deze toewijzen aan `ppid`. |
| `metadata.segment.alias` -> `list_id` | Hiermee wijst u publieksnamen van Experience Platforms toe aan gebruikers-id&#39;s in het Google-platform. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Vertelt het Google-platform wanneer gediskwalificeerde gebruikers uit segmenten moeten worden verwijderd. |

Deze toewijzingen zijn vereist door [!DNL Google Ad Manager 360] en worden automatisch door Adobe Experience Platform voor iedereen gemaakt [!DNL Google Ad Manager 360] verbindingen.

![UI-afbeelding die de toewijzingsstap voor Google Ad Manager 360 weergeeft.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Google Cloud Storage] emmertje en zorg ervoor de uitgevoerde dossiers de verwachte profielpopulaties bevatten.

## Problemen oplossen {#troubleshooting}

Voor het geval u om het even welke fouten terwijl het gebruiken van deze bestemming tegenkomt en moet uit naar of Adobe of Google reiken, houd de volgende IDs bij.

Dit zijn Google-account-id&#39;s van Adobe:

* **[!UICONTROL Account ID]**: 87933855
* **[!UICONTROL Customer ID]**: 89690775