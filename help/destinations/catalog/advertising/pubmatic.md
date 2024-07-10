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

Gebruiken [!DNL PubMatic Connect] om de waarde van de klant te maximaliseren door de programmatische digitale distributieketen van de toekomst te leveren. [!DNL PubMatic Connect] combineert platformtechnologie en specifieke service om te verbeteren hoe inventarisatie en gegevens worden verpakt en getransformeerd.

Gebruik deze bestemming om publieksgegevens naar te verzenden [!DNL PubMatic Connect] platform.

>[!IMPORTANT]
>
>De bestemmingsschakelaar en documentatiepagina worden gecreeerd en door [!DNL PubMatic] team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via `support@pubmatic.com`.

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL PubMatic Connect] doel, hier is een geval van steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Gebruikers richten op mobiele, web- en CTV-platforms {#targeting}

Uitgevers of gegevensleveranciers willen een publiek van Adobe Experience Platform naar [!DNL PubMatic Connect] om gebruikers te richten op mobiele, web- en CTV-platforms, met behulp van een groot aantal id&#39;s.

## Vereisten {#prerequisites}

Praat met uw [!DNL PubMatic] Accountmanager om ervoor te zorgen dat uw account correct is geconfigureerd en ondersteuning biedt voor instaptoegang tot publiekssegmenten. Zij zullen ook ervoor zorgen u alle relevante details hebt om deze bestemming te gebruiken en u van steun tijdens de opstelling te voorzien.

## Ondersteunde identiteiten {#supported-identities}

[!DNL PubMatic Connect] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/features/namespaces.md).

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
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
| --- | --- | --- |
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in de PubMatic Connect-bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
> Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

![Procedure voor verificatie](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL Bearer token]**: Vul het token van de gebruiker in om te verifiëren bij de bestemming.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Doelgegevens](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
- **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
- **[!UICONTROL Data partner ID]**: De id van de gegevenspartner is ingesteld in uw [!DNL PubMatic] die integratie te bevorderen.
- **[!UICONTROL Default country code]**: De standaardlandcode die op alle identiteiten moet worden toegepast als er niets in het profiel is opgegeven.
- **[!UICONTROL Account ID]**: Uw [!DNL PubMatic Connect] account-id.
- **[!UICONTROL Account type]**: Het accounttype van uw [!DNL PubMatic] platformaccount. Praat met uw [!DNL PubMatic] accountmanager als u vragen hebt waarop u kunt kiezen. De beschikbare opties zijn:
   - [!UICONTROL PUBLISHER]
   - [!UICONTROL DEMAND_PARTNER]
   - [!UICONTROL BUYER]

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
>
> - Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>
> - Om te exporteren _identiteiten_, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](../../assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Bronvelden selecteren:

- Selecteer een id (gewoonlijk naamruimten zoals IDFA of een naamruimte van een aangepaste id).

Doelvelden selecteren:

- Praat met uw [!DNL PubMatic] Accountmanager om de informatie op te vragen over welk type UID tijdens deze stap correct zal zijn.
- Selecteer de [!DNL PubMatic UID] typenummer dat overeenkomt met de id die u in de eerste stap hebt geselecteerd.

![Kenmerken en identiteiten toewijzen](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

De [!DNL PubMatic] Met UI kunt u controleren of de gegevens correct zijn geduwd en of de segmenten beschikbaar zijn. Het kan tot 24 uur duren nadat gegevens voor de [!DNL PubMatic] UI die moet worden bijgewerkt.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).
