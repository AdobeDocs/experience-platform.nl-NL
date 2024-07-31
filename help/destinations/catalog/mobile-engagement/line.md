---
keywords: mobiel;mobiele betrokkenheidsdoelen;LINE;LINE mobiele betrokkenheidsbestemming
title: LINE-verbinding
description: De bestemming van de LIJN staat u toe om profielen aan uw publiek van het Platform toe te voegen en gepersonaliseerde ervaringen aan verbonden gebruikers te leveren.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 0%

---

# [!DNL LINE] verbinding

## Overzicht {#overview}

[[!DNL LINE] ](https://line.me/en/) is een populair communicatie platform dat mensen, de diensten en de informatie verbindt en van een praatjeapp tot een hub voor vermaak, sociale, en dagelijkse activiteiten is gegroeid.

Dit [!DNL Adobe Experience Platform] [ bestemmings ](/help/destinations/home.md) hefboomwerkingen [[!DNL LINE]  Overseinen API ](https://developers.line.biz/en/reference/messaging-api/). U kunt profielen van uw publiek van het Experience Platform als verbindingen binnen [!DNL LINE] voor uw bedrijfsbehoeften activeren.

[!DNL LINE] gebruikt Béonder Tokens als authentificatiemechanisme om met [!DNL LINE] Overseinen API te communiceren. De instructies om aan uw [!DNL LINE] instantie voor authentiek te verklaren zijn verder hieronder, binnen [ voor authentiek verklaren aan bestemmings ](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Als markeerteken kunt u gebruikers in een mobiele betrokkenheidsbestemming als doel instellen, met een publiek dat is ingebouwd in [!DNL Adobe Experience Platform] . Bovendien kunt u persoonlijke ervaringen aan hen aanbieden, op basis van attributen van hun [!DNL Adobe Experience Platform] profielen, zodra het publiek en de profielen in [!DNL Adobe Experience Platform] worden bijgewerkt.

## Vereisten {#prerequisites}

### [!DNL LINE] voorwaarden {#prerequisites-destination}

Als u gegevens wilt exporteren van Platform naar uw [!DNL LINE] -account, moet u rekening houden met de volgende voorwaarden in [!DNL LINE] :

#### U moet een [!DNL LINE] -account hebben {#prerequisites-account}

Als u nog geen account hebt, moet u zich registreren en een [!DNL LINE] -account maken. Een account maken:

1. Navigeer aan de [!DNL LINE] [ rekening login ](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) pagina
2. Selecteer **[!UICONTROL Create an account]**.

#### De [!DNL LINE channel access token (long-lived)] verzamelen vanaf de [!DNL LINE] ontwikkelaarsconsole {#gather-credentials}

Om Platform toe te staan om tot [!DNL LINE] middelen toegang te hebben, zult u *[!DNL Channel access token (long-lived)]* van het gewenste [!DNL LINE] *Overseinen API* kanaal nodig hebben.

1. Login met uw [!DNL LINE] rekening aan de [[!DNL LINE]  console van de Ontwikkelaar ](https://developers.line.biz/console).
1. Daarna, heb toegang tot de *[!DNL Providers]* lijst, dan selecteer *[!DNL Provider]* van rente en selecteer ten slotte het *Overseinen API* kanaal om tot zijn montages toegang te hebben. Als u tot de ontwikkelaarsconsole voor het eerst toegang hebt volg de [[!DNL LINE]  documentatie ](https://developers.line.biz/en/docs/messaging-api/getting-started/) om de stappen te voltooien die worden vereist om een leverancier tot stand te brengen.
1. Tot slot navigeer aan de ***[!DNL Channel access token]*** sectie en kopieer de ***[!DNL Channel access token (long-lived)]*** waarde die binnen [ wordt vereist voor authentiek verklaart aan bestemmings ](#authenticate) stap.

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Uw [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Verwijs naar de [[!DNL LINE]  documentatie ](https://developers.line.biz/en/docs/messaging-api/getting-started/) voor begeleiding bij het creëren van een kanaal of het toevoegen van een kanaal aan uw bestaande [!DNL LINE] rekening door de [!DNL LINE] ontwikkelaarsconsole.

## Ondersteunde identiteiten {#supported-identities}

[!DNL LINE] ondersteunt het bijwerken en exporteren van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving |
|---|---|
| Id voor adverteerders (IFA&#39;s) | Selecteer identiteitskaart voor Advertisers (IFAs) doelidentiteit wanneer de bronidentiteiten IFA *(identiteitskaart van Apple voor Advertisers)* of GAID * (identiteitskaart van Google Advertising) namespaces zijn. |
| REGEL-gebruikersnaam | Selecteer de doelidentiteit van de gebruikersnaam wanneer de bronid&#39;s LINE-gebruikers zijn. |

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de [!DNL LINE] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Kies in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** Zoeken naar [!DNL LINE] . U kunt de locatie ook in de categorie **[!UICONTROL Mobile engagement]** vinden.

### Verifiëren voor bestemming {#authenticate}

Selecteer **[!UICONTROL Connect to destination]** als u wilt verifiëren bij het doel.
{het schermschot van het platform UI die tonen hoe te voor authentiek te verklaren.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)![

Vul de vereiste velden hieronder in.
* **[!UICONTROL Bearer token]**: Uw [!DNL LINE Channel access token (long-lived)] vanuit de [!DNL LINE] ontwikkelaarsconsole. Verwijs naar [ verzamelen geloofsbrieven ](#gather-credentials) sectie.

Als de opgegeven gegevens geldig zijn, geeft de gebruikersinterface de status **[!UICONTROL Connected]** weer met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
{het schermschot van het platform UI die de bestemmingsdetails toont.](../../assets/catalog/mobile-engagement/line/destination-details.png)![

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Audience Type]**: Selecteer **[!UICONTROL ID for Advertisers(IFAs)]** als de identiteiten u van type *identiteitskaart voor Advertisers (IFAs)* wilt uitvoeren. Selecteer **[!UICONTROL LINE user IDs]** als de identiteiten u van type *wilt uitvoeren - Gebruiker IDs*. Verwijs naar de [ Gesteunde identiteiten ](#supported-identities) sectie voor meer informatie over de identiteitstypes.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL LINE] -bestemming wilt verzenden, moet u de stap voor veldtoewijzing doorlopen. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Platform-account en de bijbehorende equivalenten van de doelbestemming. Voer de volgende stappen uit om uw XDM-velden correct toe te wijzen aan de [!DNL LINE] -doelvelden:

Afhankelijk van uw bronidentiteit moeten de volgende naamruimten voor de doelidentiteit worden toegewezen:

| Doelidentiteit | Source-veld | Doelveld |
| --- | --- | --- |
| Id voor adverteerders (IFA&#39;s) | `IDFA` of `GAID` | `LineId` |
| Gebruiker-id&#39;s voor LIJN | `UserID` | `LineId` |

Als uw doelidentiteiten *gebruiker ID&#39;s van de LIJN* zijn zult u hieronder nodig hebben:
![ het schermschot van het Platform UI die de afbeelding van het Doel tonen wanneer het gebruiken van de Gebruiker van de LIJN IDs voor doelidentiteiten.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Als uw doelidentiteit *identiteitskaart voor Advertisers (IFAs)* is zult u hieronder nodig hebben:
![ het schermschot van het Platform UI die de afbeelding van het Doel tonen wanneer het gebruiken van identiteitskaart voor Advertisers (IFAs) voor doelidentiteiten.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Gegevens exporteren valideren {#exported-data}

Wanneer de gegevensexport uit het Experience Platform is gelukt, maakt de [!DNL LINE] -bestemming een nieuw publiek in [!DNL LINE] met de geselecteerde publieksnaam.

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. In [!DNL LINE], login aan de [ console van de Manager ](https://manager.line.biz/).

1. Navigeer vervolgens naar **[!UICONTROL Data Controls]** > **[!UICONTROL Audiences]** en controleer de naam die overeenkomt met het geselecteerde publiek in de kolom **[!UICONTROL Audience name]** .

1. Het bijgewerkte volume komt overeen met de telling binnen het segment.

1. De *kolom van het Type* {zal **[!UICONTROL UserID]** vermelden als de identiteiten u uitvoerde van type *UserID* zijn. Op dezelfde manier zal de *kolom van het Type* **[!UICONTROL Mobile ad Id]** vermelden als de identiteiten u uitvoerde van type *IDFA* zijn.

Hieronder ziet u een voorbeeldinstelling in [!DNL LINE] :
![ het schermschot van de LIJN UI die het publieksvolume toont.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).
