---
title: PubMatic Connect
description: PubMatic maximaliseert klantenwaarde door de programmatic digitale marketing leveringsketen van de toekomst te leveren. PubMatic Connect combineert platformtechnologie en toegewijde service om te verbeteren hoe inventarisatie en gegevens worden verpakt en getransformeerd.
last-substantial-update: 2023-12-14T00:00:00Z
exl-id: 21e07d2c-9a6a-4cfa-a4b8-7ca48613956c
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# PubMatic Connect-doel {#pubmatic-connect}

## Overzicht {#overview}

Gebruik [!DNL PubMatic Connect] om de waarde van klanten te maximaliseren door de programmatische digitale distributieketen van de toekomst te leveren. [!DNL PubMatic Connect] combineert platformtechnologie en toegewijde service om te verbeteren hoe inventarisatie en gegevens worden verpakt en getransformeerd.

Gebruik deze bestemming om publieksgegevens naar het [!DNL PubMatic Connect] -platform te verzenden.

>[!IMPORTANT]
>
>De doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL PubMatic] . Voor vragen of updateverzoeken kunt u rechtstreeks contact opnemen via `support@pubmatic.com` .

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL PubMatic Connect] bestemming zou moeten gebruiken, is hier een geval van het steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Gebruikers richten op mobiele, web- en CTV-platforms {#targeting}

Uitgevers of gegevensleveranciers willen een publiek van Adobe Experience Platform naar [!DNL PubMatic Connect] sturen om gebruikers op mobiele, web- en CTV-platforms te bereiken met behulp van een groot aantal id&#39;s.

## Vereisten {#prerequisites}

Neem contact op met uw accountmanager van [!DNL PubMatic] om te controleren of uw account correct is geconfigureerd en ondersteuning biedt voor instaptoegang tot publiekssegmenten. Zij zullen ook ervoor zorgen u alle relevante details hebt om deze bestemming te gebruiken en u van steun tijdens de opstelling te voorzien.

## Ondersteunde identiteiten {#supported-identities}

[!DNL PubMatic Connect] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
| --------------- | ------ | --- |
| GAID | GOOGLE ADVERTISING ID | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| extern_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
| --- | --------- | ------ |
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van het Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
| --- | --- | --- |
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in de PubMatic Connect-bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
> Om met de bestemming te verbinden, hebt u de **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

![ hoe te voor authentiek te verklaren ](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL Bearer token]**: vul de token aan voor de toonder om te verifiëren bij het doel.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![ de details van de Bestemming ](../../assets/catalog/advertising/pubmatic/destination-details.png)

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

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
>
> - Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>
> - Om _identiteiten_ uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](../../assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en segmenten aan het stromen segment de uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Bronvelden selecteren:

- Selecteer een id (gewoonlijk naamruimten zoals IDFA of een naamruimte van een aangepaste id).

Doelvelden selecteren:

- Bespreek met uw accountmanager van [!DNL PubMatic] welke informatie over welk type UID tijdens deze stap correct zal zijn.
- Selecteer het [!DNL PubMatic UID] typenummer dat overeenkomt met de id die u in de eerste stap hebt geselecteerd.

![ de attributen en de identiteiten van de Kaart ](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Met de interface van [!DNL PubMatic] kunt u controleren of de gegevens correct zijn geduwd en of de segmenten beschikbaar zijn. Het kan tot 24 uur duren nadat gegevens zijn geduwd op de gebruikersinterface van [!DNL PubMatic] om te worden bijgewerkt.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).
