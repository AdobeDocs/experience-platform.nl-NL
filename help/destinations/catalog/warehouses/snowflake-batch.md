---
title: Snowflake Batch-verbinding
description: Een live Snowflake-gegevensuitwisseling maken om dagelijkse publieksupdates rechtstreeks als gedeelde tabellen in uw account te ontvangen.
last-substantial-update: 2025-10-23T00:00:00Z
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 6959ccd0-ba30-4750-a7de-d0a709292ef7
source-git-commit: 271700625e8cc1d2b5e737e89435c543caa86264
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 0%

---

# Snowflake Batch-verbinding {#snowflake-destination}

>[!AVAILABILITY]
>
>Deze bestemmingsschakelaar is in beperkte beschikbaarheid en slechts beschikbaar aan Real-Time CDP Ultimate klanten die in het [&#x200B; worden provisioned VA7 gebied &#x200B;](/help/landing/multi-cloud.md#azure-regions).

## Overzicht {#overview}

Gebruik deze bestemming om publieksgegevens naar dynamische tabellen in uw Snowflake-account te verzenden. Dynamische tabellen bieden toegang tot uw gegevens zonder dat fysieke gegevenskopieën nodig zijn.

Lees de volgende secties om te begrijpen hoe de bestemming van Snowflake werkt en hoe de gegevens tussen Adobe en Snowflake worden overgebracht.

### Hoe Snowflake data sharing werkt {#data-sharing}

Dit doel gebruikt een [!DNL Snowflake] gegevensuitwisseling, wat betekent dat er geen gegevens fysiek worden geëxporteerd of overgebracht naar uw eigen Snowflake-instantie. In plaats daarvan biedt Adobe u alleen-lezentoegang tot een live tabel die wordt gehost in de Snowflake-omgeving van Adobe. U kunt deze gedeelde tabel rechtstreeks vanaf uw Snowflake-account opvragen, maar u hebt geen eigenaar van de tabel en kunt de tabel niet wijzigen of behouden na de opgegeven bewaarperiode. Adobe beheert de levenscyclus en structuur van de gedeelde tabel volledig.

De eerste keer nadat u een gegevensstroom hebt ingesteld van Adobe naar uw Snowflake-account, wordt u gevraagd om de persoonlijke aanbieding van Adobe te accepteren.

![&#x200B; Schermafbeelding die het privé scherm van de Snowflake van de lijstgoedkeuring toont &#x200B;](../../assets/catalog/cloud-storage/snowflake-batch/snowflake-accept-listing.png)

### Bewaren van gegevens en Tijd-aan-Levende (TTL) {#ttl}

Alle gegevens die via deze integratie worden gedeeld, hebben een vaste tijd-aan-Levende (TTL) van zeven dagen. Zeven dagen na de laatste uitvoer, verloopt de dynamische lijst automatisch en wordt ontoegankelijk, ongeacht of dataflow nog actief is. Als u de gegevens langer dan zeven dagen moet bewaren, moet u de inhoud in een lijst kopiëren die u in uw eigen instantie van Snowflake bezit alvorens TTL verloopt.

>[!IMPORTANT]
>
>Als u een gegevensstroom verwijdert in Experience Platform, verdwijnt de dynamische tabel van uw Snowflake-account.

### Updategedrag van publiek {#audience-update-behavior}

Als uw publiek op [&#x200B; partijwijze &#x200B;](../../../segmentation/methods/batch-segmentation.md) wordt geëvalueerd, worden de gegevens in de gedeelde lijst verfrist om de 24 uur. Dit betekent dat er een vertraging van maximaal 24 uur kan optreden tussen wijzigingen in het lidmaatschap van het publiek en wanneer deze wijzigingen worden weerspiegeld in de gedeelde tabel.

### Batchgegevensdelingslogica {#batch-data-sharing}

Wanneer een dataflow voor het eerst voor een publiek loopt, voert het backfill uit en deelt het alle momenteel gekwalificeerde profielen. Na deze aanvankelijke backfill, verstrekt de bestemming periodieke momentopnamen van het volledige publiekslidmaatschap. Elke momentopname vervangt de vorige gegevens in de gedeelde lijst, die ervoor zorgt dat u altijd de recentste volledige mening van het publiek zonder historische gegevens ziet.

## Streaming en delen van batchgegevens {#batch-vs-streaming}

Experience Platform verstrekt twee soorten bestemmingen van Snowflake: [&#x200B; Snowflake die &#x200B;](snowflake.md) en [&#x200B; de Partij van Snowflake stromen &#x200B;](snowflake-batch.md) stroomt.

Terwijl beide bestemmingen u toegang tot uw gegevens in Snowflake op een nul-exemplaarmanier geven, zijn er sommige geadviseerde beste praktijken in termen van gebruiksgevallen voor elke schakelaar.

De lijst hieronder zal u helpen beslissen welke schakelaar aan gebruik door de scenario&#39;s te schetsen waar elke gegevens het delen methode het meest aangewezen is.

|  | Kies [&#x200B; Batch van Snowflake &#x200B;](snowflake-batch.md) wanneer u nodig hebt | Kies [&#x200B; Streaming Snowflake &#x200B;](snowflake.md) wanneer u nodig hebt |
|--------|-------------------|----------------------|
| **de frequentie van de Update** | Periodieke momentopnamen | Continue updates in realtime |
| **de presentatie van Gegevens** | Volledige publieksopname die vorige gegevens vervangt | Incrementele updates op basis van profielwijzigingen |
| **het geval van het Gebruik nadruk** | Analytische/ML-werklasten waarbij latentie niet essentieel is | Directe handelingsscenario&#39;s die updates in real time vereisen |
| **het beheer van Gegevens** | Altijd laatste volledige opname bekijken | Incrementele updates op basis van wijzigingen in het publiekslidmaatschap |
| **de scenario&#39;s van het Voorbeeld** | Bedrijfsrapportage, gegevensanalyse, modeltraining in ML | Onderdrukking van marketingcampagnes, realtime personalisatie |

Voor meer informatie over het stromen gegevens die delen, zie de [&#x200B; Snowflake Streaming verbinding &#x200B;](snowflake.md) documentatie.

## Gebruiksscenario’s {#use-cases}

Het delen van batchgegevens is ideaal voor scenario&#39;s waarbij u een volledige momentopname van uw publiek nodig hebt en realtime updates niet vereist zijn, zoals:

* **Analytische werklasten**: Wanneer het uitvoeren van gegevensanalyse, het melden, of bedrijfsintelligentietaken die een volledige mening van publieksenlidmaatschap vereisen
* **machine die werkschema&#39;s** leert: Voor de modellen van opleidingsXML of lopende voorspellende analyse die van volledige publieksmomentopnamen profiteren
* **het entrepot van Gegevens**: Wanneer u een huidig exemplaar van publieksgegevens in uw eigen instantie van Snowflake moet handhaven
* **Periodieke rapportering**: Voor regelmatige zaken die waar u de recentste publieksstaat zonder historische verandering het volgen nodig hebt
* **ETL processen**: Wanneer u publieksgegevens in partijen moet omzetten of verwerken

Het delen van batchgegevens vereenvoudigt gegevensbeheer door volledige momentopnamen te bieden, zodat incrementele updates niet handmatig hoeven te worden beheerd of wijzigingen handmatig moeten worden samengevoegd.

## Vereisten {#prerequisites}

Voordat u uw Snowflake-verbinding configureert, moet u aan de volgende voorwaarden voldoen:

* U hebt toegang tot een [!DNL Snowflake] -account.
* Je Snowflake-account is geabonneerd op privé-aanbiedingen. U of iemand in uw bedrijf die beheerdersrechten voor accounts heeft op Snowflake, kan dit configureren.

Lees de [[!DNL Snowflake]  documentatie &#x200B;](https://docs.snowflake.com/en/collaboration/consumer-listings-access#access-a-private-listing) voor meer informatie over de noodzakelijke toestemmingen.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren. De twee lijsten hieronder wijzen op welk publiek deze schakelaar steunt, door _kijkoorsprong_ en _profieltypes inbegrepen in het publiek_:

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Alle andere doelgroepen | ✓ | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [&#x200B; diverse publieksoorsprong &#x200B;](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-apps, zoals Adobe Journey Optimizer; </li><li> en meer. </li></ul> |

{style="table-layout:auto"}

Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario’s |
|--------------------|-----------|-------------|-----------|
| [&#x200B; het publiek van Mensen &#x200B;](/help/segmentation/types/people-audiences.md) | ✓ | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [&#x200B; publiek van de Rekening &#x200B;](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [&#x200B; Het publiek van het Vooruitzicht &#x200B;](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [&#x200B; de uitvoer van de Dataset &#x200B;](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het Data Lake van Adobe Experience Platform. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de [!DNL Snowflake] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Batch]** | Deze bestemming verstrekt periodieke momentopnamen van volledig publiekslidmaatschap door de gegevens van Snowflake te delen. Elke momentopname vervangt de vorige gegevens, die ervoor zorgen u altijd de recentste volledige mening van uw publiek hebt. |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Selecteer **[!UICONTROL Connect to destination]** en geef een accountnaam en (optioneel) een accountbeschrijving op om de account bij de bestemming te verifiëren.

![&#x200B; het schermschot van de Steekproef die hoe te om aan de bestemming &#x200B;](../../assets/catalog/cloud-storage/snowflake-batch/authenticate-destination.png) voor authentiek te verklaren tonen

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_snowflake_batch_accountid"
>title="Voer je Snowflake-account-id in"
>abstract="Als uw account aan een organisatie is gekoppeld, gebruikt u deze indeling: `OrganizationName.AccountName`<br><br> Als uw account niet aan een organisatie is gekoppeld, gebruikt u deze indeling: `AccountName`"

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![&#x200B; het schermschot van de Steekproef die hoe te om details voor uw bestemming te vullen &#x200B;](../../assets/catalog/cloud-storage/snowflake-batch/configure-destination-details.png) tonen

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Snowflake Account ID]**: je Snowflake-account-id. Gebruik de volgende indeling voor account-id, afhankelijk van of uw account is gekoppeld aan een organisatie:
   * Als uw rekening met een organisatie verbonden is:`OrganizationName.AccountName`.
   * Als uw rekening niet met een organisatie is verbonden:`AccountName`.
* **[!UICONTROL Select Snowflake Region]**: selecteer het gebied waar uw Snowflake-instantie is ingericht. Zie de documentatie van Snowflake [&#x200B; &#x200B;](https://docs.snowflake.com/en/user-guide/intro-regions) voor gedetailleerde informatie over gesteunde wolkengebieden.
* **[!UICONTROL Account acknowledgment]**: Nadat u **[!UICONTROL Snowflake Account ID]** hebt ingevoerd, selecteert u **[!UICONTROL Yes]** in dit vervolgkeuzemenu om te bevestigen dat de **[!UICONTROL Snowflake Account ID]** correct is en dat deze van u is.

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

Lees [&#x200B; activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Kenmerken Kaart {#map}

U kunt identiteiten en profielkenmerken naar dit doel exporteren.

![&#x200B; Experience Platform gebruikersinterfacebeeld dat het kaartscherm voor de bestemming van Snowflake toont.](../../assets/catalog/cloud-storage/snowflake-batch/mapping.png)

U kunt de [&#x200B; berekende gebiedscontrole &#x200B;](../../ui/data-transformations-calculated-fields.md) gebruiken om verrichtingen op series uit te voeren en uit te voeren.

De doelkenmerken worden automatisch in Snowflake gemaakt met de kenmerknaam die u in het veld **[!UICONTROL Attribute name]** opgeeft.

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

De gegevens worden via een dynamische tabel gefaseerd opgeslagen in uw Snowflake-account. Controleer uw Snowflake-account om te controleren of de gegevens correct zijn geëxporteerd.

### Gegevensstructuur {#data-structure}

De dynamische tabel bevat de volgende kolommen:

* **TS**: Een timestamp kolom die vertegenwoordigt wanneer elke rij het laatst werd bijgewerkt
* **de attributen van de Toewijzing**: Elk toewijzingsattribuut dat u tijdens het activeringswerkschema selecteert wordt vertegenwoordigd als kolomkopbal in Snowflake
* **het lidmaatschap van het publiek**: Het lidmaatschap aan om het even welk publiek dat aan dataflow wordt in kaart gebracht wordt vermeld via een `active` ingang in de overeenkomstige cel

![&#x200B; Schermschot die de interface van Snowflake met dynamische lijstgegevens tonen &#x200B;](../../assets/catalog/cloud-storage/snowflake-batch/data-validation.png)

## Bekende beperkingen {#known-limitations}

### Regionale beschikbaarheid {#regional-availability}

De batchbestemming [!DNL Snowflake] is momenteel alleen beschikbaar voor Real-Time CDP-klanten die zijn ingericht in het Experience Platform VA7-gebied.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).
