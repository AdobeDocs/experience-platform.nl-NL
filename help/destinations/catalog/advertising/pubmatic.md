---
title: PubMatic Connect
description: PubMatic maximaliseert klantenwaarde door de programmatic digitale marketing leveringsketen van de toekomst te leveren. PubMatic Connect combineert platformtechnologie en toegewijde service om te verbeteren hoe inventarisatie en gegevens worden verpakt en getransformeerd.
last-substantial-update: 2025-02-12T00:00:00Z
exl-id: 21e07d2c-9a6a-4cfa-a4b8-7ca48613956c
source-git-commit: 2041c06e660e24f63d4c44adc0e8f3082bb007ae
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---


# PubMatic Connect-doel {#pubmatic-connect}

## Overzicht {#overview}

Gebruik [!DNL PubMatic Connect] om de waarde van klanten te maximaliseren door de programmatische digitale distributieketen van de toekomst te leveren. [!DNL PubMatic Connect] combineert platformtechnologie en toegewijde service om te verbeteren hoe inventarisatie en gegevens worden verpakt en getransformeerd.

Er zijn twee beschikbare doelen waarmee u publieksgegevens naar het PubMatic Connect-platform kunt verzenden. De functionaliteit van de componenten verschilt enigszins:

1. PubMatic Connect

   Tijdens de eerste activering registreert deze bestemming automatisch het publiek in het PubMatic-platform en gebruikt deze de interne Adobe Experience Platform-id voor toewijzing.

2. PubMatic Connect (Custom Audience ID Mapping)

   Met deze bestemming kunt u handmatig een toewijzings-id toevoegen tijdens de activeringsworkflow. Gebruik deze bestemming wanneer de gegevens naar bestaand publiek in het platform moeten worden verzonden PubMatic of als een douane &quot;identiteitskaart van het Publiek van Source&quot;wordt vereist.

![&#x200B; zij aan zij mening van twee schakelaars PubMatic in de catalogus van bestemmingen.](/help/destinations/assets/catalog/advertising/pubmatic/two-pubmatic-connectors-side-by-side.png)

>[!IMPORTANT]
>
> De doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL PubMatic] . Voor vragen of updateverzoeken kunt u rechtstreeks contact opnemen via `support@pubmatic.com` .

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL PubMatic Connect] bestemming zou moeten gebruiken, is hier een geval van het steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Gebruikers richten op mobiele, web- en CTV-platforms {#targeting}

Uitgevers of gegevensleveranciers willen een publiek van Adobe Experience Platform naar [!DNL PubMatic Connect] sturen om gebruikers op mobiele, web- en CTV-platforms te bereiken met behulp van een groot aantal id&#39;s.

## Vereisten {#prerequisites}

Neem contact op met uw accountmanager van [!DNL PubMatic] om te controleren of uw account correct is geconfigureerd en ondersteuning biedt voor instaptoegang tot publiekssegmenten. Zij zullen ook ervoor zorgen u alle relevante details hebt om deze bestemming te gebruiken en u van steun tijdens de opstelling te voorzien.

## Ondersteunde identiteiten {#supported-identities}

[!DNL PubMatic Connect] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
| --------------- | ------------------------ | ------------------------------------------------------------------------------- |
| GAID | GOOGLE ADVERTISING ID | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| extern_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
| --------------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------- |
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
| ---------------- | ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in de PubMatic Connect-bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt die op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
> Om met de bestemming te verbinden, hebt u de **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

![&#x200B; hoe te voor authentiek te verklaren &#x200B;](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL Bearer token]**: vul de token aan voor de toonder om te verifiëren bij het doel.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![&#x200B; de details van de Bestemming &#x200B;](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
- **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
- **[!UICONTROL Data partner ID]**: De id van de gegevenspartner die voor deze integratie is ingesteld in uw [!DNL PubMatic] -account.
- **[!UICONTROL Default country code]**: De standaardlandcode die op alle identiteiten moet worden toegepast als er geen in het profiel is opgegeven.
- **[!UICONTROL Account ID]**: Uw [!DNL PubMatic Connect] account-id.
- **[!UICONTROL Account type]**: Het accounttype van uw [!DNL PubMatic] -platformaccount. Neem contact op met uw accountmanager van [!DNL PubMatic] als u vragen hebt waarop u wilt kiezen. De beschikbare opties zijn:
   - [!UICONTROL PUBLISHER]
   - [!UICONTROL DEMAND_PARTNER]
   - [!UICONTROL BUYER]

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
>
> - Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>
> - Om _identiteiten_ uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](../../assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer profielen en segmenten aan het stromen segment de uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Bronvelden selecteren:

- Selecteer een id (gewoonlijk naamruimten zoals IDFA of een naamruimte van een aangepaste id).

Doelvelden selecteren:

- Bespreek met uw accountmanager van [!DNL PubMatic] welke informatie over welk UID-type tijdens deze stap correct zal zijn.
- Selecteer het [!DNL PubMatic UID] typenummer dat overeenkomt met de id die u in de eerste stap hebt geselecteerd.

![&#x200B; de attributen en de identiteiten van de Kaart &#x200B;](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

### Publiek plannen

Als u de bestemming PubMatic Connect (Custom Audience ID Mapping) gebruikt, moet u een toewijzings-id opgeven voor elk publiek dat overeenkomt met de &#39;Source Audience ID&#39; in het PubMatic-platform.

![&#x200B; Publiek dat &#x200B;](../..//assets/catalog/advertising/pubmatic/audience-scheduling-mapping-id.png) plant

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Met de interface van [!DNL PubMatic] kunt u controleren of de gegevens correct zijn geduwd en of de segmenten beschikbaar zijn. Het kan tot 24 uur duren nadat gegevens zijn geduwd op de gebruikersinterface van [!DNL PubMatic] om te worden bijgewerkt.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).
