---
keywords: mobiel;mobiele betrokkenheidsdoelen;LINE;LINE mobiele betrokkenheidsbestemming
title: LINE-verbinding
description: De bestemming van de LIJN staat u toe om profielen aan uw publiek van het Platform toe te voegen en gepersonaliseerde ervaringen aan verbonden gebruikers te leveren.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 0%

---

# [!DNL LINE] verbinding

## Overzicht {#overview}

[[!DNL LINE]](https://line.me/en/) is een populair communicatieplatform dat mensen, services en informatie met elkaar verbindt en is uitgegroeid van een chat-app tot een hub voor entertainment, sociale en dagelijkse activiteiten.

Dit [!DNL Adobe Experience Platform] [doel](/help/destinations/home.md) gebruikt de [[!DNL LINE] Berichten-API](https://developers.line.biz/en/reference/messaging-api/). U kunt profielen van uw publiek van het Experience Platform als verbindingen binnen activeren [!DNL LINE] voor uw bedrijfsbehoeften.

[!DNL LINE] gebruikt Draaiende Tokens als authentificatiemechanisme om met het [!DNL LINE] Berichten-API. Instructies voor verificatie aan uw [!DNL LINE] instantie bevindt zich verderop, binnen [Verifiëren voor bestemming](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Als markeerteken kunt u gebruikers in een mobiele betrokkenheidsbestemming als doel instellen, met een ingebouwd publiek [!DNL Adobe Experience Platform]. Bovendien kunt u hun persoonlijke ervaringen bieden op basis van de kenmerken van hun [!DNL Adobe Experience Platform] profielen, zodra het publiek en de profielen in [!DNL Adobe Experience Platform].

## Vereisten {#prerequisites}

### [!DNL LINE] voorwaarden {#prerequisites-destination}

Houd rekening met de volgende voorwaarden in [!DNL LINE]om gegevens van Platform naar uw [!DNL LINE] account:

#### U hebt een [!DNL LINE] account {#prerequisites-account}

U moet zich registreren en een [!DNL LINE] account, als u er nog geen hebt. Een account maken:

1. Ga naar de [!DNL LINE] [aanmelding bij account](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) page
2. Selecteer **[!UICONTROL Create an account]**.

#### De [!DNL LINE channel access token (long-lived)] van de [!DNL LINE] ontwikkelingsconsole {#gather-credentials}

Toegang verlenen aan platform [!DNL LINE] bronnen, hebt u de *[!DNL Channel access token (long-lived)]* van het gewenste [!DNL LINE] *Berichten-API* kanaal.

1. Meld u aan met uw [!DNL LINE] aan de [[!DNL LINE] Developer Console](https://developers.line.biz/console).
1. Ga vervolgens naar de *[!DNL Providers]* en selecteert u vervolgens de *[!DNL Provider]* van belang zijn en ten slotte de *Berichten-API* kanaal voor toegang tot de instellingen. Als u de ontwikkelaarsconsole voor het eerst opent, volgt u de [[!DNL LINE] documentatie](https://developers.line.biz/en/docs/messaging-api/getting-started/) om de stappen te voltooien die nodig zijn om een provider te maken.
1. Ten slotte navigeert u naar de ***[!DNL Channel access token]*** en kopieer de ***[!DNL Channel access token (long-lived)]*** waarde vereist binnen [Verifiëren voor bestemming](#authenticate) stap.

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Uw [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Zie de [[!DNL LINE] documentatie](https://developers.line.biz/en/docs/messaging-api/getting-started/) voor hulp bij het maken van een kanaal of het toevoegen van een kanaal aan uw bestaande [!DNL LINE] via de [!DNL LINE] ontwikkelaarsconsole.

## Ondersteunde identiteiten {#supported-identities}

[!DNL LINE] ondersteunt het bijwerken en exporteren van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|---|
| Id voor adverteerders (IFA&#39;s) | Selecteer de doelidentiteit van de id voor adverteerders (IFA&#39;s) wanneer de bronid IFA is *(Apple-id voor adverteerders)* of GAID *(Google Advertising ID) naamruimten. |
| REGEL-gebruikersnaam | Selecteer de doelidentiteit van de gebruikersnaam wanneer de bronid&#39;s LINE-gebruikers zijn. |

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in het dialoogvenster [!DNL LINE] bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Within **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** zoeken naar [!DNL LINE]. U kunt de locatie ook onder de **[!UICONTROL Mobile engagement]** categorie.

### Verifiëren voor bestemming {#authenticate}

Om voor authentiek te verklaren aan de bestemming, uitgezocht **[!UICONTROL Connect to destination]**.
![Schermopname van de gebruikersinterface van het platform waarin wordt getoond hoe te voor authentiek te verklaren.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Vul de vereiste velden hieronder in.
* **[!UICONTROL Bearer token]**: Uw [!DNL LINE Channel access token (long-lived)] van de [!DNL LINE] ontwikkelaarsconsole. Zie de [gegevens verzamelen](#gather-credentials) sectie.

Als de verstrekte gegevens geldig zijn, geeft de interface een **[!UICONTROL Connected]** status met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
![Platform UI het schermschot die de bestemmingsdetails tonen.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Audience Type]**: Select **[!UICONTROL ID for Advertisers(IFAs)]** als de identiteiten die u wilt exporteren van het type zijn *Id voor adverteerders (IFA&#39;s)*. Selecteren **[!UICONTROL LINE user IDs]** als de identiteiten die u wilt exporteren van het type zijn *REGEL-gebruikersnaam*. Zie de [Ondersteunde identiteiten](#supported-identities) voor meer informatie over de identiteitstypen.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Profielen en doelgroepen activeren voor het streamen van doelgroepen voor het exporteren van bestanden](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL LINE] doel, moet u door de stap van de gebiedstoewijzing gaan. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Platform-account en de bijbehorende equivalenten van de doelbestemming. Uw XDM-velden op de juiste wijze toewijzen aan de [!DNL LINE] doelvelden, voer de volgende stappen uit:

Afhankelijk van uw bronidentiteit moeten de volgende naamruimten voor de doelidentiteit worden toegewezen: | Doelidentiteit | Bronveld | Doelveld | | — | — | — | | Id voor adverteerders (IFA&#39;s) | `IDFA` of `GAID` | `LineId` | | Gebruiker-id&#39;s voor LIJN | `UserID` | `LineId` |

Als uw doelidentiteiten *Gebruiker-id&#39;s van regel* U hebt het volgende nodig:
![Het het schermschot van het platform UI die de afbeelding van het Doel toont wanneer het gebruiken van LIJNGebruiker IDs voor doelidentiteiten.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Als uw doelidentiteit *Id voor adverteerders (IFA&#39;s)* U hebt het volgende nodig:
![Het het schermschot van het platform UI die de afbeelding van het Doel toont wanneer het gebruiken van identiteitskaart voor Advertisers (IFAs) voor doelidentiteiten.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Gegevens exporteren valideren {#exported-data}

Als gegevens uit Experience Platform zijn geëxporteerd, wordt de [!DNL LINE] doel maakt een nieuw publiek binnen [!DNL LINE] met de naam van het geselecteerde publiek.

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. In [!DNL LINE], meldt u zich aan bij [Manager-console](https://manager.line.biz/).

1. Ga vervolgens naar **[!UICONTROL Data Controls]** > **[!UICONTROL Audiences]** en controleer de naam die overeenkomt met het geselecteerde publiek in het deelvenster **[!UICONTROL Audience name]** kolom.

1. Het bijgewerkte volume komt overeen met de telling binnen het segment.

1. De *Type* kolom zal vermelden **[!UICONTROL UserID]** als de id&#39;s die u hebt geëxporteerd van het type zijn *GebruikerID*. Evenzo geldt het *Type* kolom zal vermelden **[!UICONTROL Mobile ad Id]** als de id&#39;s die u hebt geëxporteerd van het type zijn *IDFA*.

Een voorbeeldinstelling binnen [!DNL LINE] wordt hieronder weergegeven:
![De het schermschot van de LIJN UI die het publiekvolume toont.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).
