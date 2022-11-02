---
keywords: doel verbinden;doel verbindt;hoe te bestemming verbinden
title: Een nieuwe doelverbinding maken
type: Tutorial
description: Leer hoe u verbinding maakt met een doel in Adobe Experience Platform, waarschuwingen inschakelt en marketingacties instelt voor de verbonden bestemming.
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 434b9ed4f64320b5fd73b752716cb34a8e48aec9
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 0%

---

# Een nieuwe doelverbinding maken

>[!IMPORTANT]
> 
>* Als u verbinding wilt maken met een doel, hebt u de **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om met een bestemming te verbinden die de uitvoer van datasets steunt, hebt u nodig **[!UICONTROL Manage and Activate Dataset Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.


## Overzicht {#overview}

Voordat u publieksgegevens naar een bestemming kunt verzenden, moet u een verbinding naar het doelplatform instellen. In dit artikel wordt uitgelegd hoe u een nieuwe doelverbinding instelt, waarnaar u segmenten kunt activeren of gegevenssets kunt exporteren met de gebruikersinterface van Adobe Experience Platform.

## Het gewenste doel in de catalogus zoeken {#setup}

1. Ga naar **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab.

   ![Screenshot van de interface van het Experience Platform, met daarin de pagina met de doelcatalogus.](../assets/ui/connect-destinations/catalog.png)

2. De kaarten van de bestemming in de catalogus zouden verschillende actiecontroles kunnen hebben, afhankelijk van of u een bestaande verbinding aan de bestemming hebt en of de bestemmingen het activeren segmenten, het uitvoeren van datasets, of allebei steunen. U zou om het even welke volgende controles voor bestemmingskaarten kunnen zien:

   * **[!UICONTROL Set up]**. Een verbinding moet eerst opstelling aan deze bestemming zijn alvorens u segmenten kunt activeren of datasets uitvoeren.
   * **[!UICONTROL Activate]**. Er is al een verbinding ingesteld met dit doel. Deze bestemming steunt segmentactivering en de uitvoer van datasets.
   * **[!UICONTROL Activate segments]**. Er is al een verbinding ingesteld met dit doel. Deze bestemming steunt slechts segmentactivering.

   Voor meer informatie over het verschil tussen deze controles, kunt u ook naar verwijzen [Catalogus](../ui/destinations-workspace.md#catalog) in de documentatie van de doelwerkruimte.

   Selecteer **[!UICONTROL Set up]**, **[!UICONTROL Activate]**, of **[!UICONTROL Activate segments]**, afhankelijk van welk besturingselement beschikbaar is.

   ![Screenshot van het Experience Platform UI, die de pagina van de bestemmingscatalogus met de benadrukte controle van de Opstelling toont.](../assets/ui/connect-destinations/set-up.png)

   ![Screenshot van het Experience Platform UI, die de pagina van de bestemmingscatalogus met de Activate segmenten benadrukte controle toont.](../assets/ui/connect-destinations/activate-segments.png)

3. Als u **[!UICONTROL Set up]**, gaat u verder met de volgende stap, naar [authenticate](#authenticate) naar de bestemming.

   Als u **[!UICONTROL Activate]**, **[!UICONTROL Activate segments]**, of **[!UICONTROL Export datasets]** kunt u nu een lijst met bestaande doelverbindingen zien.

   Selecteren **[!UICONTROL Configure new destination]** om een nieuwe verbinding aan de bestemming te vestigen.

   ![Screenshot van het Experience Platform UI, die een lijst van beschikbare bestemmingen en vormt nieuwe benadrukte bestemmingscontrole toont.](../assets/ui/connect-destinations/configure-new-destination.png)

## Verifiëren voor bestemming {#authenticate}

De eerste stap in het verbinden met een bestemming moet aan het bestemmingsplatform voor authentiek verklaren.

Afhankelijk van de bestemming waarmee u verbindt, zou u aan de pagina van de bestemmingspartner kunnen worden gebracht voor authentiek te verklaren, of u zou kunnen worden gevraagd om authentificatiegeloofsbrieven direct in het werkschema van het Platform in te voeren. Hieronder ziet u een voorbeeld van de vereiste invoer voor verificatie bij een [!DNL Amazon S3] bestemming. Gedetailleerde instructies over de vereiste invoer worden gegeven in elke pagina van de bestemmingsdocumentatie (zie, bijvoorbeeld, de authentificatiesectie voor [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) en voor [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate)).

**[!DNL Amazon S3]vereiste en optionele verificatieparameters**

![Afbeelding die de vereiste en optionele invoerparameters weergeeft bij verificatie bij een Amazon S3-bestemming.](../assets/ui/connect-destinations/authenticate-amazon-s3-example.png)

## Verbindingsparameters instellen {#set-up-connection-parameters}

Als u al verificatie hebt ingesteld op de bestemming, kunt u doorgaan met het bestaande account of kunt u een nieuw account instellen.

Afhankelijk van het doel waarmee u verbinding maakt, wordt u mogelijk gevraagd verschillende typen verbindingsparameters in te voeren. Wanneer u bijvoorbeeld verbinding maakt met een [!DNL Amazon S3] bestemming, wordt u gevraagd details over te verstrekken [!DNL Amazon S3] Naam emmertje en mappad waar bestanden worden gedeponeerd. Hieronder vindt u twee voorbeelden van vereiste invoer voor een [!DNL Amazon S3] bestemming en [!DNL Trade Desk] bestemming. Gedetailleerde instructies over de vereiste invoer worden gegeven op elke pagina van de doeldocumentatie.

>[!IMPORTANT]
>
>De onderstaande afbeeldingen worden alleen ter illustratie gebruikt. De details van de bestemmingsverbinding variëren tussen bestemmingen. Voor gedetailleerde informatie over de verbindingsdetails voor uw bestemming, lees **Verbinden met de bestemming** sectie in elke [doelcatalogus](../catalog/overview.md) pagina (bijvoorbeeld [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect), [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect), of [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)).

**[!DNL Amazon S3]vereiste en optionele invoerparameters**

![Afbeelding die de vereiste en optionele invoerparameters weergeeft wanneer verbinding wordt gemaakt met een Amazon S3-doel.](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]vereiste en optionele invoerparameters**

![Afbeelding die de vereiste en optionele invoerparameters weergeeft wanneer verbinding wordt gemaakt met een doel van een handelsbureau.](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### Opties voor bestandsindeling instellen voor geëxporteerde bestanden {#file-formatting-and-compression-options}

Voor op bestanden gebaseerde doelen kunt u verschillende instellingen configureren die betrekking hebben op de indeling en comprimeren van de geëxporteerde bestanden. Voor meer informatie over alle beschikbare opties voor opmaak en compressie leest u de [Zelfstudie over het configureren van opties voor bestandsindeling voor op bestanden gebaseerde doelen](/help/destinations/ui/batch-destinations-file-formatting-options.md).

![Afbeelding waarin de selectie van het bestandstype en de verschillende opties voor CSV-bestanden worden weergegeven.](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### De bestemmingsverbinding van de opstelling voor segmentactivering of datasetuitvoer {#segment-activation-or-dataset-exports}

Sommige op dossier-gebaseerde bestemmingen steunen segmentactivering evenals datasetuitvoer. Voor die bestemmingen, kunt u verkiezen of om een verbinding tot stand te brengen die u toelaat om segmenten te activeren of datasets uit te voeren.

![Afbeelding die het besturingselement voor het selecteren van gegevenstypen weergeeft. Hiermee kunnen gebruikers kiezen tussen segmentactivering en het exporteren van gegevenssets.](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### Doelwaarschuwingen inschakelen {#enable-alerts}

1. (Optioneel) Selecteer de waarschuwingen voor de doelgegevensstroom waarop u zich wilt abonneren. U kunt zich op alarm abonneren wanneer het creëren van een gegevensstroom om waakzame berichten betreffende de status, het succes, of het mislukken van uw looppas te ontvangen. De beschikbare waarschuwingen verschillen afhankelijk van het doeltype (bestandsgebaseerd of streaming) waarmee u verbinding maakt. Lezen [Abonneren op in-context-bestemmingswaarschuwingen](alerts.md) voor gedetailleerde informatie over waarschuwingen over bestemmingsgegevensstroom.

   ![Het Configure nieuwe bestemmingsdialoog met de in-context benadrukte opties van het bestemmingsalarm.](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. Selecteer **[!UICONTROL Next]**.

   ![Het Configure nieuwe bestemmingsdialoog met de Volgende benadrukte controle, toestaand de gebruiker om aan de volgende stap in het werkschema te werk te gaan.](../assets/ui/connect-destinations/next.png)

## marketingacties selecteren {#select-marketing-actions}

1. Selecteer de marketingacties die van toepassing zijn op de gegevens die u naar de bestemming wilt exporteren. Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Zie voor meer informatie over marketingacties de [overzicht van beleidsregels voor gegevensgebruik](../../data-governance/policies/overview.md) pagina.

   ![Het Configure nieuwe bestemmingsdialoog met de beschikbare benadrukte marketing acties. De beschikbare besturingselementen voor het voltooien van de workflow Verbinding maken met bestemming worden ook gemarkeerd.](../assets/ui/connect-destinations/governance.png)

2. Selecteren **[!UICONTROL Save & Exit]** om de bestemmingsconfiguratie te bewaren, of te selecteren **[!UICONTROL Next]** om door te gaan naar de publieksgegevens [activeringsstroom](activation-overview.md).

## Volgende stappen {#next-steps}

Door dit document te lezen, hebt u geleerd hoe te om Experience Platform UI te gebruiken om een verbinding aan een bestemming te vestigen. Ter herinnering, variëren de beschikbare en vereiste verbindingsparameters van bestemming tot bestemming. U moet ook de pagina met doeldocumentatie raadplegen in het dialoogvenster [doelcatalogus](/help/destinations/catalog/overview.md) voor specifieke informatie over de vereiste inputs en beschikbare opties per bestemmingstype.

Vervolgens kunt u doorgaan naar [activeren, segmenten](/help/destinations/ui/activation-overview.md) of [gegevensbestanden exporteren](/help/destinations/ui/export-datasets.md) naar uw bestemming.