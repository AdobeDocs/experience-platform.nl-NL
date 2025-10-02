---
title: Snowflake Streaming-verbinding
description: Exporteer gegevens naar je Snowflake-account met privéaanbiedingen.
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4a00e46a-dedb-4dd3-b496-b0f4185ea9b0
source-git-commit: eed90a5ce988acafface0bac9191f1b3ae28f90c
workflow-type: tm+mt
source-wordcount: '1411'
ht-degree: 0%

---

# Snowflake Streaming-verbinding {#snowflake-destination}

>[!IMPORTANT]
>
>Deze doelconnector is in bèta beschikbaar voor Real-Time CDP Ultimate-klanten. De functionaliteit en documentatie kunnen worden gewijzigd.

## Overzicht {#overview}

Gebruik de bestemmingsschakelaar van Snowflake om gegevens naar de instantie van Snowflake van Adobe uit te voeren, die Adobe dan met uw instantie door [&#x200B; privé lijsten &#x200B;](https://other-docs.snowflake.com/en/collaboration/collaboration-listings-about) deelt.

Lees de volgende secties om te begrijpen hoe de bestemming van Snowflake werkt en hoe de gegevens tussen Adobe en Snowflake worden overgebracht.

### Hoe Snowflake data sharing werkt {#data-sharing}

Dit doel gebruikt een [!DNL Snowflake] gegevensuitwisseling, wat betekent dat er geen gegevens fysiek worden geëxporteerd of overgebracht naar uw eigen Snowflake-instantie. In plaats daarvan biedt Adobe u alleen-lezentoegang tot een live tabel die wordt gehost in de Snowflake-omgeving van Adobe. U kunt deze gedeelde tabel rechtstreeks vanaf uw Snowflake-account opvragen, maar u hebt geen eigenaar van de tabel en kunt de tabel niet wijzigen of behouden na de opgegeven bewaarperiode. Adobe beheert de levenscyclus en structuur van de gedeelde tabel volledig.

De eerste keer dat je gegevens van een Adobe Snowflake-exemplaar naar jou deelt, wordt je gevraagd om de privé-aanbieding van Adobe te accepteren.

![&#x200B; Schermafbeelding die het privé scherm van de Snowflake van de lijstgoedkeuring toont &#x200B;](../../assets/catalog/cloud-storage/snowflake/snowflake-accept-listing.png)

### Bewaren van gegevens en Tijd-aan-Levende (TTL) {#ttl}

Alle gegevens die via deze integratie worden gedeeld, hebben een vaste tijd-aan-Levende (TTL) van zeven dagen. Zeven dagen na de laatste uitvoer, verloopt de gedeelde lijst automatisch en wordt ontoegankelijk, ongeacht of dataflow nog actief is. Als u de gegevens langer dan zeven dagen moet bewaren, moet u de inhoud in een lijst kopiëren die u in uw eigen instantie van Snowflake bezit alvorens TTL verloopt.

### Updategedrag van publiek {#audience-update-behavior}

Als uw publiek op [&#x200B; partijwijze &#x200B;](../../../segmentation/methods/batch-segmentation.md) wordt geëvalueerd, worden de gegevens in de gedeelde lijst verfrist om de 24 uur. Dit betekent dat er een vertraging van maximaal 24 uur kan optreden tussen wijzigingen in het lidmaatschap van het publiek en wanneer deze wijzigingen worden weerspiegeld in de gedeelde tabel.

### Incrementele exportlogica {#incremental-export}

Wanneer een dataflow voor het eerst voor een publiek loopt, voert het backfill uit en deelt het alle momenteel gekwalificeerde profielen. Na deze eerste backfill worden alleen incrementele updates weergegeven in de gedeelde tabel. Dit betekent profielen die worden toegevoegd aan of verwijderd uit het publiek. Deze aanpak zorgt voor efficiënte updates en zorgt ervoor dat de gedeelde tabel up-to-date blijft.

## Streaming en delen van batchgegevens {#batch-vs-streaming}

Experience Platform verstrekt twee soorten bestemmingen van Snowflake: [&#x200B; Snowflake die &#x200B;](snowflake.md) en [&#x200B; de Partij van Snowflake stromen &#x200B;](../cloud-storage/snowflake-batch.md) stroomt.

De lijst hieronder zal u helpen beslissen welke bestemming te gebruiken door de scenario&#39;s te schetsen waar elke gegevens het delen methode het meest aangewezen is.

|  | Kies [&#x200B; Batch van Snowflake &#x200B;](../cloud-storage/snowflake-batch.md) wanneer u nodig hebt | Kies [&#x200B; Streaming Snowflake &#x200B;](snowflake.md) wanneer u nodig hebt |
|--------|-------------------|----------------------|
| **de frequentie van de Update** | Periodieke momentopnamen | Continue updates in realtime |
| **de presentatie van Gegevens** | Volledige publieksopname die vorige gegevens vervangt | Incrementele updates op basis van profielwijzigingen |
| **het geval van het Gebruik nadruk** | Analytische/ML-werklasten waarbij latentie niet essentieel is | Directe handelingsscenario&#39;s die updates in real time vereisen |
| **het beheer van Gegevens** | Altijd laatste volledige opname bekijken | Incrementele updates op basis van wijzigingen in het publiekslidmaatschap |
| **de scenario&#39;s van het Voorbeeld** | Bedrijfsrapportage, gegevensanalyse, modeltraining in ML | Onderdrukking van marketingcampagnes, realtime personalisatie |

Voor meer informatie over partijgegevens die delen, zie de [&#x200B; de verbinding van de Partij van Snowflake &#x200B;](../cloud-storage/snowflake-batch.md) documentatie.

## Gebruiksscenario’s {#use-cases}

Het delen van streaming gegevens is ideaal voor scenario&#39;s waarin u directe updates nodig hebt wanneer een profiel zijn lidmaatschap of andere kenmerken wijzigt. Dit is essentieel voor gebruiksgevallen die realtime responsiviteit vereisen, zoals:

* **de campagneonderdrukking van de Marketing**: onderdruk onmiddellijk marketing campagnes voor gebruikers die specifieke acties, zoals het ondertekenen omhoog voor de dienst of het maken van een aankoop hebben ondernomen
* **Realtime verpersoonlijking**: De ervaringen van de gebruiker van de update onmiddellijk wanneer de profielattributen veranderen, zoals wanneer een gebruiker een website bezoekt, een productpagina bekijkt, of punten aan een het winkelwagentje toevoegt
* **Onmiddellijke actiescenario&#39;s**: Voer snelle onderdrukking en het retargeting uit die op gegevens in real time wordt gebaseerd om vertragingen te verminderen en marketing campagnes te verzekeren zijn relevanter en tijdiger
* **Efficiëntie en nuance**: Laat grotere efficiency en nuance in marketing inspanningen toe door snelle reactie op veranderingen van het gebruikersgedrag toe te staan
* **Real-time optimalisering van de klantenreis**: De ervaringen van de klant van de update onmiddellijk wanneer het segmentlidmaatschap of de profielattributen veranderen

Het stromen gegevens het delen verstrekt ononderbroken updates die op segmentveranderingen, veranderingen van de identiteitskaart, of attributenveranderingen worden gebaseerd, die het voor scenario&#39;s geschikt maken waar de latentie kritiek is en de directe updates worden vereist.

## Vereisten {#prerequisites}

Voordat u uw Snowflake-verbinding configureert, moet u aan de volgende voorwaarden voldoen:

* U hebt toegang tot een [!DNL Snowflake] -account.
* Je Snowflake-account is geabonneerd op privé-aanbiedingen. U of iemand in uw bedrijf die beheerdersrechten voor accounts heeft op Snowflake, kan dit configureren.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren. De twee lijsten hieronder wijzen op welk publiek deze schakelaar steunt, door _kijkoorsprong_ en _profieltypes inbegrepen in het publiek_:

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Alle andere doelgroepen | ✓ | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [&#x200B; diverse publieksoorsprong &#x200B;](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-apps, zoals Adobe Journey Optimizer; </li><li> en meer. </li></ul> |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de [!DNL Snowflake] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Selecteer **[!UICONTROL Connect to destination]** als u wilt verifiëren bij het doel.

![&#x200B; het schermschot van de Steekproef die hoe te om aan de bestemming &#x200B;](../../assets/catalog/cloud-storage/snowflake/authenticate-destination.png) voor authentiek te verklaren tonen

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_snowflake_accountID"
>title="Voer je Snowflake-account-id in"
>abstract="Als uw account aan een organisatie is gekoppeld, gebruikt u deze indeling: `OrganizationName.AccountName`<br><br> Als uw account niet aan een organisatie is gekoppeld, gebruikt u deze indeling: `AccountName`"

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![&#x200B; het schermschot van de Steekproef die hoe te om details voor uw bestemming te vullen &#x200B;](../../assets/catalog/cloud-storage/snowflake/configure-destination-details.png) tonen

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Snowflake Account ID]**: je Snowflake-account-id. Gebruik de volgende indeling voor account-id, afhankelijk van of uw account is gekoppeld aan een organisatie:
   * Als uw rekening met een organisatie verbonden is:`OrganizationName.AccountName`.
   * Als uw rekening niet met een organisatie is verbonden:`AccountName`.
* **[!UICONTROL Account acknowledgment]**: Schakel de optie voor het bevestigen van de Snowflake-account-id in om te bevestigen dat uw account-id correct is en van u afkomstig is.

>[!IMPORTANT]
>
> Speciale tekens die worden gebruikt in de doelnaam en de naam van de Experience Platform-sandbox worden automatisch omgezet in onderstrepingstekens (`_`) in Snowflake. Gebruik geen speciale tekens in de naam van het doel en de sandbox om verwarring te voorkomen.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, lees de gids over [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Kenmerken Kaart {#map}

De Snowflake-bestemming ondersteunt het toewijzen van profielkenmerken aan aangepaste kenmerken.

![&#x200B; Experience Platform gebruikersinterfacebeeld dat het kaartscherm voor de bestemming van Snowflake toont.](../../assets/catalog/cloud-storage/snowflake/mapping.png)

De doelkenmerken worden automatisch in Snowflake gemaakt met de kenmerknaam die u in het veld **[!UICONTROL Attribute name]** opgeeft.

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Controleer uw Snowflake-account om te controleren of de gegevens correct zijn geëxporteerd.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).
